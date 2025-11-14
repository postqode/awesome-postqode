# React Best Practices

## Objective
Establish modern React development patterns using functional components, hooks, and TypeScript for maintainable, performant applications.

## Context
Apply these practices when:
- Building React applications (v18+)
- Using TypeScript for type safety
- Working with functional components and hooks
- Implementing state management and side effects

## Guidelines

### Core Principles

1. **Functional Components Only**: Use functional components with hooks instead of class components
2. **TypeScript First**: Leverage TypeScript for type safety and better developer experience
3. **Composition Over Inheritance**: Build complex UIs from simple, reusable components
4. **Immutable State**: Never mutate state directly, always create new objects/arrays
5. **Single Responsibility**: Each component should have one clear purpose

### Do This ✅

**Pattern 1: Functional Components with TypeScript**
```typescript
interface UserCardProps {
  name: string;
  email: string;
  onEdit?: () => void;
}

export const UserCard: React.FC<UserCardProps> = ({ name, email, onEdit }) => {
  return (
    <div className="user-card">
      <h3>{name}</h3>
      <p>{email}</p>
      {onEdit && <button onClick={onEdit}>Edit</button>}
    </div>
  );
};
```

**Pattern 2: Custom Hooks for Logic Reuse**
```typescript
function useLocalStorage<T>(key: string, initialValue: T) {
  const [storedValue, setStoredValue] = useState<T>(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(error);
      return initialValue;
    }
  });

  const setValue = (value: T | ((val: T) => T)) => {
    try {
      const valueToStore = value instanceof Function ? value(storedValue) : value;
      setStoredValue(valueToStore);
      window.localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (error) {
      console.error(error);
    }
  };

  return [storedValue, setValue] as const;
}
```

**Pattern 3: Proper useEffect Dependencies**
```typescript
function UserProfile({ userId }: { userId: string }) {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    let cancelled = false;

    async function fetchUser() {
      setLoading(true);
      try {
        const data = await api.getUser(userId);
        if (!cancelled) {
          setUser(data);
        }
      } catch (error) {
        if (!cancelled) {
          console.error('Failed to fetch user:', error);
        }
      } finally {
        if (!cancelled) {
          setLoading(false);
        }
      }
    }

    fetchUser();

    return () => {
      cancelled = true;
    };
  }, [userId]); // Only re-run when userId changes

  if (loading) return <div>Loading...</div>;
  if (!user) return <div>User not found</div>;

  return <div>{user.name}</div>;
}
```

### Avoid This ❌

**Anti-pattern 1: Class Components**
```typescript
// Avoid - use functional components instead
class UserCard extends React.Component<UserCardProps> {
  render() {
    return <div>{this.props.name}</div>;
  }
}
```

**Anti-pattern 2: Direct State Mutation**
```typescript
// Avoid - mutating state directly
function TodoList() {
  const [todos, setTodos] = useState<Todo[]>([]);

  const addTodo = (text: string) => {
    todos.push({ id: Date.now(), text }); // ❌ Direct mutation
    setTodos(todos); // ❌ Won't trigger re-render
  };

  // Correct approach
  const addTodoCorrect = (text: string) => {
    setTodos([...todos, { id: Date.now(), text }]); // ✅ New array
  };
}
```

**Anti-pattern 3: Missing useEffect Dependencies**
```typescript
// Avoid - missing dependencies
function SearchResults({ query }: { query: string }) {
  const [results, setResults] = useState([]);

  useEffect(() => {
    fetchResults(query).then(setResults);
  }, []); // ❌ Missing 'query' dependency

  // Correct
  useEffect(() => {
    fetchResults(query).then(setResults);
  }, [query]); // ✅ Include all dependencies
}
```

## Detailed Examples

### Example 1: Form Handling with Validation
```typescript
interface FormData {
  email: string;
  password: string;
}

interface FormErrors {
  email?: string;
  password?: string;
}

export const LoginForm: React.FC = () => {
  const [formData, setFormData] = useState<FormData>({
    email: '',
    password: '',
  });
  const [errors, setErrors] = useState<FormErrors>({});
  const [isSubmitting, setIsSubmitting] = useState(false);

  const validate = (): boolean => {
    const newErrors: FormErrors = {};

    if (!formData.email) {
      newErrors.email = 'Email is required';
    } else if (!/\S+@\S+\.\S+/.test(formData.email)) {
      newErrors.email = 'Email is invalid';
    }

    if (!formData.password) {
      newErrors.password = 'Password is required';
    } else if (formData.password.length < 8) {
      newErrors.password = 'Password must be at least 8 characters';
    }

    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();

    if (!validate()) return;

    setIsSubmitting(true);
    try {
      await api.login(formData);
      // Handle success
    } catch (error) {
      setErrors({ email: 'Invalid credentials' });
    } finally {
      setIsSubmitting(false);
    }
  };

  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    const { name, value } = e.target;
    setFormData(prev => ({ ...prev, [name]: value }));
    // Clear error when user starts typing
    if (errors[name as keyof FormErrors]) {
      setErrors(prev => ({ ...prev, [name]: undefined }));
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <input
          type="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
          placeholder="Email"
        />
        {errors.email && <span className="error">{errors.email}</span>}
      </div>
      <div>
        <input
          type="password"
          name="password"
          value={formData.password}
          onChange={handleChange}
          placeholder="Password"
        />
        {errors.password && <span className="error">{errors.password}</span>}
      </div>
      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? 'Logging in...' : 'Login'}
      </button>
    </form>
  );
};
```

### Example 2: Data Fetching with Error Handling
```typescript
interface UseApiResult<T> {
  data: T | null;
  loading: boolean;
  error: Error | null;
  refetch: () => void;
}

function useApi<T>(url: string): UseApiResult<T> {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);
  const [refetchIndex, setRefetchIndex] = useState(0);

  useEffect(() => {
    let cancelled = false;

    async function fetchData() {
      setLoading(true);
      setError(null);

      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        const json = await response.json();
        if (!cancelled) {
          setData(json);
        }
      } catch (e) {
        if (!cancelled) {
          setError(e instanceof Error ? e : new Error('Unknown error'));
        }
      } finally {
        if (!cancelled) {
          setLoading(false);
        }
      }
    }

    fetchData();

    return () => {
      cancelled = true;
    };
  }, [url, refetchIndex]);

  const refetch = () => setRefetchIndex(prev => prev + 1);

  return { data, loading, error, refetch };
}

// Usage
function UserList() {
  const { data: users, loading, error, refetch } = useApi<User[]>('/api/users');

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  if (!users) return <div>No users found</div>;

  return (
    <div>
      <button onClick={refetch}>Refresh</button>
      <ul>
        {users.map(user => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
}
```

## Best Practices

### 1. Component Organization
- Keep components small and focused (< 200 lines)
- Extract complex logic into custom hooks
- Use composition to build complex UIs
- Co-locate related files (component, styles, tests)

### 2. State Management
- Use `useState` for local component state
- Use `useReducer` for complex state logic
- Consider Context API for shared state
- Use external libraries (Redux, Zustand) for global state when needed

### 3. Performance Optimization
- Use `React.memo` for expensive components
- Use `useMemo` for expensive calculations
- Use `useCallback` for function props to memoized components
- Lazy load components with `React.lazy` and `Suspense`

### 4. Type Safety
- Define interfaces for all props
- Use TypeScript's utility types (`Partial`, `Pick`, `Omit`)
- Avoid `any` type - use `unknown` if type is truly unknown
- Use generics for reusable components

### 5. Error Handling
- Use Error Boundaries for component errors
- Handle async errors in useEffect
- Provide user-friendly error messages
- Log errors for debugging

## Common Pitfalls

### Pitfall 1: Infinite Loops in useEffect
```typescript
// ❌ Creates infinite loop
useEffect(() => {
  setCount(count + 1); // Updates state, triggers re-render, runs effect again
});

// ✅ Correct - with dependency array
useEffect(() => {
  // Only runs once on mount
}, []);
```

### Pitfall 2: Stale Closures
```typescript
// ❌ Stale closure
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setCount(count + 1); // Always uses initial count value
    }, 1000);
    return () => clearInterval(interval);
  }, []); // Missing count dependency

  // ✅ Correct - use functional update
  useEffect(() => {
    const interval = setInterval(() => {
      setCount(c => c + 1); // Uses current value
    }, 1000);
    return () => clearInterval(interval);
  }, []);
}
```

### Pitfall 3: Not Cleaning Up Side Effects
```typescript
// ❌ Memory leak - no cleanup
useEffect(() => {
  const subscription = api.subscribe(data => setData(data));
}, []);

// ✅ Correct - cleanup function
useEffect(() => {
  const subscription = api.subscribe(data => setData(data));
  return () => subscription.unsubscribe();
}, []);
```

## References
- [React Official Documentation](https://react.dev)
- [TypeScript React Cheatsheet](https://react-typescript-cheatsheet.netlify.app/)
- [React Hooks Documentation](https://react.dev/reference/react)
- [React Performance Optimization](https://react.dev/learn/render-and-commit)

## Related Rules
- [TypeScript Standards](./typescript-standards.md)
- [Testing Strategies](../testing/testing-strategies.md)
- [Performance Optimization](../testing/performance-optimization.md)
