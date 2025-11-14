# React Native Best Practices

## Objective
Establish React Native development standards for building performant, maintainable cross-platform mobile applications.

## Context
Apply when:
- Building React Native applications (v0.70+)
- Developing for iOS and Android platforms
- Implementing navigation and state management
- Optimizing mobile app performance

## Guidelines

### Core Principles

1. **Platform-Specific Code**: Use platform-specific code when necessary
2. **Performance First**: Optimize for mobile constraints
3. **Native Modules**: Leverage native capabilities when needed
4. **Responsive Design**: Support various screen sizes and orientations
5. **Offline Support**: Handle network connectivity gracefully

### Do This ✅

**Pattern 1: Component Structure**
```typescript
import React from 'react';
import { View, Text, StyleSheet, Platform } from 'react-native';

interface UserCardProps {
  name: string;
  email: string;
  onPress?: () => void;
}

export const UserCard: React.FC<UserCardProps> = ({ name, email, onPress }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.name}>{name}</Text>
      <Text style={styles.email}>{email}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    padding: 16,
    backgroundColor: '#fff',
    borderRadius: 8,
    ...Platform.select({
      ios: {
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.1,
        shadowRadius: 4,
      },
      android: {
        elevation: 4,
      },
    }),
  },
  name: {
    fontSize: 18,
    fontWeight: '600',
    marginBottom: 4,
  },
  email: {
    fontSize: 14,
    color: '#666',
  },
});
```

**Pattern 2: Navigation with React Navigation**
```typescript
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

type RootStackParamList = {
  Home: undefined;
  Profile: { userId: string };
  Settings: undefined;
};

const Stack = createNativeStackNavigator<RootStackParamList>();

export function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Profile" component={ProfileScreen} />
        <Stack.Screen name="Settings" component={SettingsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

// Type-safe navigation
import { NativeStackNavigationProp } from '@react-navigation/native-stack';

type ProfileScreenNavigationProp = NativeStackNavigationProp<
  RootStackParamList,
  'Profile'
>;

interface ProfileScreenProps {
  navigation: ProfileScreenNavigationProp;
  route: RouteProp<RootStackParamList, 'Profile'>;
}
```

**Pattern 3: Performance Optimization**
```typescript
import React, { useMemo, useCallback } from 'react';
import { FlatList, View, Text } from 'react-native';

interface Item {
  id: string;
  title: string;
}

export const OptimizedList: React.FC<{ data: Item[] }> = ({ data }) => {
  // Memoize render item
  const renderItem = useCallback(({ item }: { item: Item }) => (
    <View>
      <Text>{item.title}</Text>
    </View>
  ), []);

  // Memoize key extractor
  const keyExtractor = useCallback((item: Item) => item.id, []);

  return (
    <FlatList
      data={data}
      renderItem={renderItem}
      keyExtractor={keyExtractor}
      removeClippedSubviews={true}
      maxToRenderPerBatch={10}
      updateCellsBatchingPeriod={50}
      initialNumToRender={10}
      windowSize={5}
    />
  );
};
```

### Avoid This ❌

**Anti-pattern 1: Inline Styles**
```typescript
// ❌ Avoid - creates new object on every render
<View style={{ padding: 16, backgroundColor: '#fff' }}>
  <Text>Content</Text>
</View>

// ✅ Use StyleSheet
const styles = StyleSheet.create({
  container: {
    padding: 16,
    backgroundColor: '#fff',
  },
});

<View style={styles.container}>
  <Text>Content</Text>
</View>
```

**Anti-pattern 2: Not Using FlatList for Long Lists**
```typescript
// ❌ Avoid - renders all items at once
{items.map(item => (
  <ItemComponent key={item.id} item={item} />
))}

// ✅ Use FlatList for virtualization
<FlatList
  data={items}
  renderItem={({ item }) => <ItemComponent item={item} />}
  keyExtractor={item => item.id}
/>
```

## Best Practices

### 1. State Management
```typescript
// Use Context for global state
import { createContext, useContext, useState } from 'react';

interface AuthContextType {
  user: User | null;
  login: (credentials: Credentials) => Promise<void>;
  logout: () => void;
}

const AuthContext = createContext<AuthContextType | undefined>(undefined);

export const AuthProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [user, setUser] = useState<User | null>(null);

  const login = async (credentials: Credentials) => {
    const user = await api.login(credentials);
    setUser(user);
  };

  const logout = () => setUser(null);

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within AuthProvider');
  }
  return context;
};
```

### 2. Platform-Specific Code
```typescript
// Platform-specific components
import { Platform } from 'react-native';

const Component = Platform.select({
  ios: () => require('./ComponentIOS').default,
  android: () => require('./ComponentAndroid').default,
})();

// Platform-specific styles
const styles = StyleSheet.create({
  container: {
    ...Platform.select({
      ios: {
        paddingTop: 20,
      },
      android: {
        paddingTop: 0,
      },
    }),
  },
});

// Platform-specific files
// Component.ios.tsx
// Component.android.tsx
```

### 3. Image Optimization
```typescript
import { Image } from 'react-native';
import FastImage from 'react-native-fast-image';

// Use FastImage for better performance
<FastImage
  source={{
    uri: imageUrl,
    priority: FastImage.priority.normal,
  }}
  resizeMode={FastImage.resizeMode.cover}
  style={styles.image}
/>

// Optimize image sizes
const imageSource = {
  uri: `${baseUrl}/image.jpg`,
  width: 300,
  height: 200,
};
```

### 4. Async Storage
```typescript
import AsyncStorage from '@react-native-async-storage/async-storage';

// Store data
const storeData = async (key: string, value: any) => {
  try {
    await AsyncStorage.setItem(key, JSON.stringify(value));
  } catch (error) {
    console.error('Error storing data:', error);
  }
};

// Retrieve data
const getData = async (key: string) => {
  try {
    const value = await AsyncStorage.getItem(key);
    return value ? JSON.parse(value) : null;
  } catch (error) {
    console.error('Error retrieving data:', error);
    return null;
  }
};
```

### 5. Keyboard Handling
```typescript
import { KeyboardAvoidingView, Platform } from 'react-native';

<KeyboardAvoidingView
  behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
  style={styles.container}
>
  <TextInput placeholder="Enter text" />
</KeyboardAvoidingView>
```

### 6. Permissions
```typescript
import { PermissionsAndroid, Platform } from 'react-native';

const requestCameraPermission = async () => {
  if (Platform.OS === 'android') {
    try {
      const granted = await PermissionsAndroid.request(
        PermissionsAndroid.PERMISSIONS.CAMERA,
        {
          title: 'Camera Permission',
          message: 'App needs access to your camera',
          buttonNeutral: 'Ask Me Later',
          buttonNegative: 'Cancel',
          buttonPositive: 'OK',
        }
      );
      return granted === PermissionsAndroid.RESULTS.GRANTED;
    } catch (err) {
      console.warn(err);
      return false;
    }
  }
  return true; // iOS handles permissions differently
};
```

### 7. Deep Linking
```typescript
import { Linking } from 'react-native';

// Handle deep links
useEffect(() => {
  const handleDeepLink = (event: { url: string }) => {
    const url = event.url;
    // Parse and navigate based on URL
  };

  Linking.addEventListener('url', handleDeepLink);

  // Check if app was opened from a deep link
  Linking.getInitialURL().then(url => {
    if (url) {
      handleDeepLink({ url });
    }
  });

  return () => {
    Linking.removeEventListener('url', handleDeepLink);
  };
}, []);
```

## Common Pitfalls

### Pitfall 1: Memory Leaks
```typescript
// ❌ Avoid - doesn't cleanup
useEffect(() => {
  const subscription = api.subscribe(data => setData(data));
}, []);

// ✅ Cleanup subscriptions
useEffect(() => {
  const subscription = api.subscribe(data => setData(data));
  return () => subscription.unsubscribe();
}, []);
```

### Pitfall 2: Not Handling Safe Area
```typescript
// ❌ Avoid - content hidden by notch
<View>
  <Text>Header</Text>
</View>

// ✅ Use SafeAreaView
import { SafeAreaView } from 'react-native-safe-area-context';

<SafeAreaView edges={['top']}>
  <Text>Header</Text>
</SafeAreaView>
```

### Pitfall 3: Blocking Main Thread
```typescript
// ❌ Avoid - heavy computation on main thread
const processData = (data) => {
  // Heavy computation
  return result;
};

// ✅ Use InteractionManager
import { InteractionManager } from 'react-native';

useEffect(() => {
  InteractionManager.runAfterInteractions(() => {
    const result = processData(data);
    setResult(result);
  });
}, [data]);
```

## Essential Libraries

- **Navigation**: `@react-navigation/native`
- **State Management**: `zustand`, `redux-toolkit`
- **Networking**: `axios`, `react-query`
- **Forms**: `react-hook-form`
- **UI Components**: `react-native-paper`, `react-native-elements`
- **Icons**: `react-native-vector-icons`
- **Images**: `react-native-fast-image`
- **Storage**: `@react-native-async-storage/async-storage`
- **Animations**: `react-native-reanimated`

## References
- [React Native Documentation](https://reactnative.dev/)
- [React Navigation](https://reactnavigation.org/)
- [Performance Optimization](https://reactnative.dev/docs/performance)

## Related Rules
- [React Best Practices](../web/react-best-practices.md)
- [TypeScript Standards](../web/typescript-standards.md)
- [Testing Strategies](../testing/testing-strategies.md)
