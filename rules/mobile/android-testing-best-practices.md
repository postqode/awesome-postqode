# Android Testing Best Practices

## Objective
Establish comprehensive testing standards for Android applications using JUnit, Espresso, and modern testing frameworks.

## Context
Apply when:
- Testing Android applications (API 21+)
- Writing unit, integration, and UI tests
- Implementing test automation for Android
- Setting up CI/CD for Android testing

## Guidelines

### Core Principles

1. **Test Pyramid**: More unit tests, fewer instrumented tests
2. **Fast Feedback**: Keep tests fast and reliable
3. **Isolation**: Tests should be independent
4. **Maintainability**: Write readable, maintainable tests
5. **Real Device Testing**: Test on actual devices when possible

### Do This ✅

**Pattern 1: Unit Testing with JUnit**
```kotlin
import org.junit.Before
import org.junit.Test
import org.junit.Assert.*
import org.mockito.Mock
import org.mockito.Mockito.*
import org.mockito.MockitoAnnotations

class UserViewModelTest {
    @Mock
    private lateinit var userRepository: UserRepository
    
    private lateinit var viewModel: UserViewModel
    
    @Before
    fun setup() {
        MockitoAnnotations.openMocks(this)
        viewModel = UserViewModel(userRepository)
    }
    
    @Test
    fun `fetchUser success returns user data`() {
        // Given
        val expectedUser = User(id = "1", name = "John Doe")
        `when`(userRepository.getUser("1")).thenReturn(Result.success(expectedUser))
        
        // When
        viewModel.fetchUser("1")
        
        // Then
        assertEquals(expectedUser, viewModel.user.value)
        assertFalse(viewModel.isLoading.value)
        assertNull(viewModel.error.value)
    }
    
    @Test
    fun `fetchUser failure sets error state`() {
        // Given
        val error = Exception("Network error")
        `when`(userRepository.getUser("1")).thenReturn(Result.failure(error))
        
        // When
        viewModel.fetchUser("1")
        
        // Then
        assertNull(viewModel.user.value)
        assertFalse(viewModel.isLoading.value)
        assertNotNull(viewModel.error.value)
    }
}
```

**Pattern 2: UI Testing with Espresso**
```kotlin
import androidx.test.espresso.Espresso.onView
import androidx.test.espresso.action.ViewActions.*
import androidx.test.espresso.assertion.ViewAssertions.matches
import androidx.test.espresso.matcher.ViewMatchers.*
import androidx.test.ext.junit.rules.ActivityScenarioRule
import androidx.test.ext.junit.runners.AndroidJUnit4
import org.junit.Rule
import org.junit.Test
import org.junit.runner.RunWith

@RunWith(AndroidJUnit4::class)
class LoginActivityTest {
    
    @get:Rule
    val activityRule = ActivityScenarioRule(LoginActivity::class.java)
    
    @Test
    fun loginFlow_validCredentials_showsWelcomeMessage() {
        // Given
        val email = "user@example.com"
        val password = "password123"
        
        // When
        onView(withId(R.id.emailEditText))
            .perform(typeText(email), closeSoftKeyboard())
        
        onView(withId(R.id.passwordEditText))
            .perform(typeText(password), closeSoftKeyboard())
        
        onView(withId(R.id.loginButton))
            .perform(click())
        
        // Then
        onView(withId(R.id.welcomeTextView))
            .check(matches(isDisplayed()))
            .check(matches(withText("Welcome!")))
    }
    
    @Test
    fun loginFlow_invalidCredentials_showsError() {
        // Given
        val email = "invalid@example.com"
        val password = "wrong"
        
        // When
        onView(withId(R.id.emailEditText))
            .perform(typeText(email), closeSoftKeyboard())
        
        onView(withId(R.id.passwordEditText))
            .perform(typeText(password), closeSoftKeyboard())
        
        onView(withId(R.id.loginButton))
            .perform(click())
        
        // Then
        onView(withText("Invalid credentials"))
            .check(matches(isDisplayed()))
    }
}
```

**Pattern 3: Testing with Compose**
```kotlin
import androidx.compose.ui.test.*
import androidx.compose.ui.test.junit4.createComposeRule
import org.junit.Rule
import org.junit.Test

class UserProfileScreenTest {
    
    @get:Rule
    val composeTestRule = createComposeRule()
    
    @Test
    fun userProfileScreen_displaysUserInfo() {
        // Given
        val user = User(id = "1", name = "John Doe", email = "john@example.com")
        
        // When
        composeTestRule.setContent {
            UserProfileScreen(user = user)
        }
        
        // Then
        composeTestRule
            .onNodeWithText("John Doe")
            .assertIsDisplayed()
        
        composeTestRule
            .onNodeWithText("john@example.com")
            .assertIsDisplayed()
    }
    
    @Test
    fun userProfileScreen_editButtonClick_navigatesToEdit() {
        // Given
        val user = User(id = "1", name = "John Doe", email = "john@example.com")
        var editClicked = false
        
        // When
        composeTestRule.setContent {
            UserProfileScreen(
                user = user,
                onEditClick = { editClicked = true }
            )
        }
        
        composeTestRule
            .onNodeWithContentDescription("Edit profile")
            .performClick()
        
        // Then
        assert(editClicked)
    }
}
```

### Avoid This ❌

**Anti-pattern 1: Testing Implementation Details**
```kotlin
// ❌ Avoid - testing private methods
@Test
fun testPrivateMethod() {
    val result = viewModel.privateMethod()
    assertEquals(expectedValue, result)
}

// ✅ Test public behavior
@Test
fun testPublicBehavior() {
    viewModel.performAction()
    assertEquals(State.COMPLETED, viewModel.state.value)
}
```

**Anti-pattern 2: Hardcoded Delays**
```kotlin
// ❌ Avoid - arbitrary sleep
Thread.sleep(3000)
onView(withId(R.id.resultText)).check(matches(isDisplayed()))

// ✅ Use IdlingResource or proper waits
onView(withId(R.id.resultText))
    .check(matches(isDisplayed()))
```

## Best Practices

### 1. Test Organization
```kotlin
class FeatureTest {
    // Test lifecycle
    @Before
    fun setup() {
        // Setup code
    }
    
    @After
    fun tearDown() {
        // Cleanup code
    }
    
    // Success cases
    @Test
    fun `feature success case`() { }
    
    // Failure cases
    @Test
    fun `feature failure case`() { }
    
    // Edge cases
    @Test
    fun `feature edge case`() { }
    
    // Helper methods
    private fun setupMockData() { }
}
```

### 2. Mocking with Mockito
```kotlin
interface UserService {
    suspend fun fetchUser(id: String): Result<User>
}

class MockUserService : UserService {
    var userToReturn: User? = null
    var errorToReturn: Exception? = null
    var fetchUserCallCount = 0
    
    override suspend fun fetchUser(id: String): Result<User> {
        fetchUserCallCount++
        
        return when {
            errorToReturn != null -> Result.failure(errorToReturn!!)
            userToReturn != null -> Result.success(userToReturn!!)
            else -> Result.failure(Exception("No data configured"))
        }
    }
}
```

### 3. Coroutine Testing
```kotlin
import kotlinx.coroutines.ExperimentalCoroutinesApi
import kotlinx.coroutines.test.*
import org.junit.Rule

@ExperimentalCoroutinesApi
class CoroutineViewModelTest {
    
    @get:Rule
    val mainDispatcherRule = MainDispatcherRule()
    
    @Test
    fun `fetchData updates state correctly`() = runTest {
        // Given
        val viewModel = MyViewModel(repository)
        
        // When
        viewModel.fetchData()
        
        // Then
        assertEquals(DataState.Success, viewModel.state.value)
    }
}

// MainDispatcherRule for testing
@ExperimentalCoroutinesApi
class MainDispatcherRule(
    private val dispatcher: TestDispatcher = StandardTestDispatcher()
) : TestWatcher() {
    override fun starting(description: Description) {
        Dispatchers.setMain(dispatcher)
    }
    
    override fun finished(description: Description) {
        Dispatchers.resetMain()
    }
}
```

### 4. Testing Room Database
```kotlin
import androidx.room.Room
import androidx.test.core.app.ApplicationProvider
import androidx.test.ext.junit.runners.AndroidJUnit4
import org.junit.After
import org.junit.Before
import org.junit.Test
import org.junit.runner.RunWith

@RunWith(AndroidJUnit4::class)
class UserDaoTest {
    private lateinit var database: AppDatabase
    private lateinit var userDao: UserDao
    
    @Before
    fun setup() {
        database = Room.inMemoryDatabaseBuilder(
            ApplicationProvider.getApplicationContext(),
            AppDatabase::class.java
        ).allowMainThreadQueries().build()
        
        userDao = database.userDao()
    }
    
    @After
    fun tearDown() {
        database.close()
    }
    
    @Test
    fun insertUser_retrievesUser() = runBlocking {
        // Given
        val user = User(id = "1", name = "John Doe", email = "john@example.com")
        
        // When
        userDao.insert(user)
        val retrieved = userDao.getUser("1")
        
        // Then
        assertEquals(user, retrieved)
    }
}
```

### 5. Testing Navigation
```kotlin
import androidx.navigation.testing.TestNavHostController
import androidx.test.core.app.ApplicationProvider

@Test
fun clickButton_navigatesToDetailScreen() {
    // Given
    val navController = TestNavHostController(
        ApplicationProvider.getApplicationContext()
    )
    
    composeTestRule.setContent {
        navController.setGraph(R.navigation.nav_graph)
        NavHost(navController = navController, startDestination = "home") {
            composable("home") { HomeScreen(navController) }
            composable("detail") { DetailScreen() }
        }
    }
    
    // When
    composeTestRule
        .onNodeWithText("View Details")
        .performClick()
    
    // Then
    assertEquals("detail", navController.currentBackStackEntry?.destination?.route)
}
```

### 6. Testing ViewModels with LiveData
```kotlin
import androidx.arch.core.executor.testing.InstantTaskExecutorRule
import org.junit.Rule

class ViewModelTest {
    
    @get:Rule
    val instantTaskExecutorRule = InstantTaskExecutorRule()
    
    @Test
    fun `liveData updates correctly`() {
        // Given
        val viewModel = MyViewModel()
        val observer = mock<Observer<String>>()
        viewModel.data.observeForever(observer)
        
        // When
        viewModel.updateData("test")
        
        // Then
        verify(observer).onChanged("test")
    }
}
```

### 7. Screenshot Testing
```kotlin
import com.github.takahirom.roborazzi.captureRoboImage
import org.junit.Test
import org.junit.runner.RunWith
import org.robolectric.RobolectricTestRunner

@RunWith(RobolectricTestRunner::class)
class ScreenshotTest {
    
    @Test
    fun userProfileScreen_lightMode() {
        composeTestRule.setContent {
            AppTheme(darkTheme = false) {
                UserProfileScreen(user = testUser)
            }
        }
        
        composeTestRule.onRoot().captureRoboImage()
    }
    
    @Test
    fun userProfileScreen_darkMode() {
        composeTestRule.setContent {
            AppTheme(darkTheme = true) {
                UserProfileScreen(user = testUser)
            }
        }
        
        composeTestRule.onRoot().captureRoboImage()
    }
}
```

## UI Testing Best Practices

### 1. Page Object Pattern
```kotlin
class LoginPage {
    fun enterEmail(email: String) {
        onView(withId(R.id.emailEditText))
            .perform(typeText(email), closeSoftKeyboard())
    }
    
    fun enterPassword(password: String) {
        onView(withId(R.id.passwordEditText))
            .perform(typeText(password), closeSoftKeyboard())
    }
    
    fun clickLogin() {
        onView(withId(R.id.loginButton))
            .perform(click())
    }
    
    fun login(email: String, password: String) {
        enterEmail(email)
        enterPassword(password)
        clickLogin()
    }
    
    fun assertWelcomeMessageDisplayed() {
        onView(withId(R.id.welcomeTextView))
            .check(matches(isDisplayed()))
    }
}

// Usage in tests
@Test
fun testLogin() {
    val loginPage = LoginPage()
    loginPage.login("user@example.com", "password123")
    loginPage.assertWelcomeMessageDisplayed()
}
```

### 2. Custom Matchers
```kotlin
fun withRecyclerView(recyclerViewId: Int): RecyclerViewMatcher {
    return RecyclerViewMatcher(recyclerViewId)
}

class RecyclerViewMatcher(private val recyclerViewId: Int) {
    fun atPosition(position: Int): Matcher<View> {
        return atPositionOnView(position, -1)
    }
    
    fun atPositionOnView(position: Int, targetViewId: Int): Matcher<View> {
        return object : TypeSafeMatcher<View>() {
            override fun describeTo(description: Description) {
                description.appendText("RecyclerView with id: $recyclerViewId at position: $position")
            }
            
            override fun matchesSafely(view: View): Boolean {
                // Implementation
                return true
            }
        }
    }
}

// Usage
onView(withRecyclerView(R.id.recyclerView).atPosition(0))
    .check(matches(hasDescendant(withText("Item 1"))))
```

### 3. IdlingResource for Async Operations
```kotlin
class SimpleIdlingResource : IdlingResource {
    @Volatile
    private var callback: IdlingResource.ResourceCallback? = null
    
    @Volatile
    private var isIdle = true
    
    override fun getName(): String = this::class.java.simpleName
    
    override fun isIdleNow(): Boolean = isIdle
    
    override fun registerIdleTransitionCallback(callback: IdlingResource.ResourceCallback?) {
        this.callback = callback
    }
    
    fun setIdleState(isIdle: Boolean) {
        this.isIdle = isIdle
        if (isIdle) {
            callback?.onTransitionToIdle()
        }
    }
}

// Usage in test
@Test
fun testWithIdlingResource() {
    val idlingResource = SimpleIdlingResource()
    IdlingRegistry.getInstance().register(idlingResource)
    
    // Perform test
    
    IdlingRegistry.getInstance().unregister(idlingResource)
}
```

## Common Pitfalls

### Pitfall 1: Not Cleaning Up
```kotlin
// ❌ Avoid - state leaks between tests
companion object {
    var sharedData = mutableListOf<String>()
}

@Test
fun testOne() {
    sharedData.add("test1")
}

// ✅ Clean up properly
@After
fun tearDown() {
    sharedData.clear()
}
```

### Pitfall 2: Flaky Tests
```kotlin
// ❌ Avoid - race conditions
@Test
fun testFlaky() {
    viewModel.startAsyncOperation()
    assertTrue(viewModel.isComplete) // May fail
}

// ✅ Wait for completion
@Test
fun testReliable() = runTest {
    viewModel.startAsyncOperation()
    advanceUntilIdle()
    assertTrue(viewModel.isComplete)
}
```

### Pitfall 3: Testing Android Framework
```kotlin
// ❌ Avoid - testing framework code
@Test
fun testTextViewBehavior() {
    val textView = TextView(context)
    textView.text = "Test"
    assertEquals("Test", textView.text)
}

// ✅ Test your code
@Test
fun testViewConfiguration() {
    val view = MyCustomView(context)
    view.configure("Test")
    assertEquals("Test", view.displayText)
    assertTrue(view.isConfigured)
}
```

## CI/CD Integration

### 1. Gradle Configuration
```kotlin
android {
    testOptions {
        unitTests {
            isIncludeAndroidResources = true
            isReturnDefaultValues = true
        }
        
        animationsDisabled = true
    }
}

dependencies {
    // Unit testing
    testImplementation("junit:junit:4.13.2")
    testImplementation("org.mockito:mockito-core:5.0.0")
    testImplementation("org.jetbrains.kotlinx:kotlinx-coroutines-test:1.7.3")
    
    // Instrumented testing
    androidTestImplementation("androidx.test.ext:junit:1.1.5")
    androidTestImplementation("androidx.test.espresso:espresso-core:3.5.1")
    androidTestImplementation("androidx.compose.ui:ui-test-junit4:1.5.4")
}
```

### 2. GitHub Actions
```yaml
name: Android Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Set up JDK
        uses: actions/setup-java@v2
        with:
          java-version: '17'
          distribution: 'adopt'
      
      - name: Run unit tests
        run: ./gradlew testDebugUnitTest
      
      - name: Run instrumented tests
        uses: reactivecircus/android-emulator-runner@v2
        with:
          api-level: 29
          script: ./gradlew connectedDebugAndroidTest
```

## Essential Tools

- **JUnit**: Unit testing framework
- **Espresso**: UI testing framework
- **Compose Test**: Jetpack Compose testing
- **Mockito/MockK**: Mocking framework
- **Robolectric**: Android unit tests without emulator
- **Roborazzi**: Screenshot testing
- **Turbine**: Flow testing
- **Truth**: Fluent assertions

## References
- [Android Testing Documentation](https://developer.android.com/training/testing)
- [Espresso Guide](https://developer.android.com/training/testing/espresso)
- [Compose Testing](https://developer.android.com/jetpack/compose/testing)

## Related Rules
- [React Native Best Practices](./react-native-best-practices.md)
- [iOS Testing Best Practices](./ios-testing-best-practices.md)
- [Testing Strategies](../testing/testing-strategies.md)
