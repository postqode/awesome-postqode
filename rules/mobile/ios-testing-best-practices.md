# iOS Testing Best Practices

## Objective
Establish comprehensive testing standards for iOS applications using XCTest, XCUITest, and modern testing frameworks.

## Context
Apply when:
- Testing iOS applications (iOS 14+)
- Writing unit, integration, and UI tests
- Implementing test automation for iOS
- Setting up CI/CD for iOS testing

## Guidelines

### Core Principles

1. **Test Pyramid**: More unit tests, fewer UI tests
2. **Fast Feedback**: Keep tests fast and reliable
3. **Isolation**: Tests should be independent
4. **Maintainability**: Write readable, maintainable tests
5. **Real Device Testing**: Test on actual devices when possible

### Do This ✅

**Pattern 1: Unit Testing with XCTest**
```swift
import XCTest
@testable import YourApp

class UserViewModelTests: XCTestCase {
    var sut: UserViewModel!
    var mockService: MockUserService!
    
    override func setUp() {
        super.setUp()
        mockService = MockUserService()
        sut = UserViewModel(service: mockService)
    }
    
    override func tearDown() {
        sut = nil
        mockService = nil
        super.tearDown()
    }
    
    func testFetchUser_Success() {
        // Given
        let expectedUser = User(id: "1", name: "John Doe")
        mockService.userToReturn = expectedUser
        
        // When
        let expectation = self.expectation(description: "User fetched")
        sut.fetchUser(id: "1") { result in
            // Then
            switch result {
            case .success(let user):
                XCTAssertEqual(user.id, expectedUser.id)
                XCTAssertEqual(user.name, expectedUser.name)
            case .failure:
                XCTFail("Expected success")
            }
            expectation.fulfill()
        }
        
        waitForExpectations(timeout: 1.0)
    }
    
    func testFetchUser_Failure() {
        // Given
        mockService.shouldFail = true
        
        // When
        let expectation = self.expectation(description: "User fetch failed")
        sut.fetchUser(id: "1") { result in
            // Then
            switch result {
            case .success:
                XCTFail("Expected failure")
            case .failure(let error):
                XCTAssertNotNil(error)
            }
            expectation.fulfill()
        }
        
        waitForExpectations(timeout: 1.0)
    }
}
```

**Pattern 2: UI Testing with XCUITest**
```swift
import XCTest

class LoginUITests: XCTestCase {
    var app: XCUIApplication!
    
    override func setUp() {
        super.setUp()
        continueAfterFailure = false
        app = XCUIApplication()
        app.launchArguments = ["UI-Testing"]
        app.launch()
    }
    
    func testLoginFlow_ValidCredentials() {
        // Given
        let emailField = app.textFields["emailTextField"]
        let passwordField = app.secureTextFields["passwordTextField"]
        let loginButton = app.buttons["loginButton"]
        
        // When
        emailField.tap()
        emailField.typeText("user@example.com")
        
        passwordField.tap()
        passwordField.typeText("password123")
        
        loginButton.tap()
        
        // Then
        let welcomeLabel = app.staticTexts["welcomeLabel"]
        XCTAssertTrue(welcomeLabel.waitForExistence(timeout: 5))
        XCTAssertEqual(welcomeLabel.label, "Welcome!")
    }
    
    func testLoginFlow_InvalidCredentials() {
        // Given
        let emailField = app.textFields["emailTextField"]
        let passwordField = app.secureTextFields["passwordTextField"]
        let loginButton = app.buttons["loginButton"]
        
        // When
        emailField.tap()
        emailField.typeText("invalid@example.com")
        
        passwordField.tap()
        passwordField.typeText("wrong")
        
        loginButton.tap()
        
        // Then
        let errorAlert = app.alerts["Error"]
        XCTAssertTrue(errorAlert.waitForExistence(timeout: 5))
        XCTAssertTrue(errorAlert.staticTexts["Invalid credentials"].exists)
    }
}
```

**Pattern 3: Snapshot Testing**
```swift
import XCTest
import SnapshotTesting
@testable import YourApp

class UserProfileSnapshotTests: XCTestCase {
    func testUserProfileView_LightMode() {
        // Given
        let user = User(id: "1", name: "John Doe", email: "john@example.com")
        let viewController = UserProfileViewController(user: user)
        
        // When/Then
        assertSnapshot(matching: viewController, as: .image(on: .iPhone13))
    }
    
    func testUserProfileView_DarkMode() {
        // Given
        let user = User(id: "1", name: "John Doe", email: "john@example.com")
        let viewController = UserProfileViewController(user: user)
        viewController.overrideUserInterfaceStyle = .dark
        
        // When/Then
        assertSnapshot(matching: viewController, as: .image(on: .iPhone13))
    }
}
```

### Avoid This ❌

**Anti-pattern 1: Testing Implementation Details**
```swift
// ❌ Avoid - testing private methods
func testPrivateMethod() {
    let result = sut.privateMethod()
    XCTAssertEqual(result, expectedValue)
}

// ✅ Test public behavior
func testPublicBehavior() {
    sut.performAction()
    XCTAssertEqual(sut.state, .completed)
}
```

**Anti-pattern 2: Hardcoded Waits**
```swift
// ❌ Avoid - arbitrary sleep
sleep(3)
XCTAssertTrue(element.exists)

// ✅ Use proper expectations
let element = app.buttons["myButton"]
XCTAssertTrue(element.waitForExistence(timeout: 5))
```

## Best Practices

### 1. Test Organization
```swift
// MARK: - Test Lifecycle
override func setUp() {
    super.setUp()
    // Setup code
}

override func tearDown() {
    // Cleanup code
    super.tearDown()
}

// MARK: - Success Cases
func testFeature_Success() { }

// MARK: - Failure Cases
func testFeature_Failure() { }

// MARK: - Edge Cases
func testFeature_EdgeCase() { }

// MARK: - Helper Methods
private func setupMockData() { }
```

### 2. Mocking and Stubbing
```swift
protocol UserServiceProtocol {
    func fetchUser(id: String, completion: @escaping (Result<User, Error>) -> Void)
}

class MockUserService: UserServiceProtocol {
    var userToReturn: User?
    var errorToReturn: Error?
    var fetchUserCallCount = 0
    
    func fetchUser(id: String, completion: @escaping (Result<User, Error>) -> Void) {
        fetchUserCallCount += 1
        
        if let error = errorToReturn {
            completion(.failure(error))
        } else if let user = userToReturn {
            completion(.success(user))
        }
    }
}
```

### 3. Async Testing
```swift
// Using XCTestExpectation
func testAsyncOperation() {
    let expectation = self.expectation(description: "Async operation")
    
    sut.performAsyncOperation { result in
        XCTAssertNotNil(result)
        expectation.fulfill()
    }
    
    waitForExpectations(timeout: 5.0)
}

// Using async/await (iOS 13+)
func testAsyncAwait() async throws {
    let result = try await sut.performAsyncOperation()
    XCTAssertNotNil(result)
}
```

### 4. Testing ViewControllers
```swift
class ViewControllerTests: XCTestCase {
    var sut: MyViewController!
    
    override func setUp() {
        super.setUp()
        let storyboard = UIStoryboard(name: "Main", bundle: nil)
        sut = storyboard.instantiateViewController(withIdentifier: "MyViewController") as? MyViewController
        sut.loadViewIfNeeded()
    }
    
    func testViewDidLoad() {
        // Then
        XCTAssertNotNil(sut.tableView)
        XCTAssertEqual(sut.title, "My View")
    }
}
```

### 5. Testing Network Calls
```swift
class NetworkTests: XCTestCase {
    var sut: NetworkManager!
    var mockSession: MockURLSession!
    
    override func setUp() {
        super.setUp()
        mockSession = MockURLSession()
        sut = NetworkManager(session: mockSession)
    }
    
    func testFetchData_Success() {
        // Given
        let expectedData = """
        {"id": "1", "name": "John"}
        """.data(using: .utf8)
        mockSession.data = expectedData
        mockSession.response = HTTPURLResponse(
            url: URL(string: "https://api.example.com")!,
            statusCode: 200,
            httpVersion: nil,
            headerFields: nil
        )
        
        // When
        let expectation = self.expectation(description: "Data fetched")
        sut.fetchData { result in
            // Then
            switch result {
            case .success(let data):
                XCTAssertEqual(data, expectedData)
            case .failure:
                XCTFail("Expected success")
            }
            expectation.fulfill()
        }
        
        waitForExpectations(timeout: 1.0)
    }
}
```

### 6. Accessibility Testing
```swift
func testAccessibility() {
    let button = app.buttons["loginButton"]
    XCTAssertTrue(button.isAccessibilityElement)
    XCTAssertEqual(button.accessibilityLabel, "Login")
    XCTAssertEqual(button.accessibilityHint, "Tap to login")
    XCTAssertEqual(button.accessibilityTraits, .button)
}
```

### 7. Performance Testing
```swift
func testPerformance_DataProcessing() {
    measure {
        // Code to measure performance
        sut.processLargeDataSet()
    }
}

func testPerformance_WithMetrics() {
    let options = XCTMeasureOptions()
    options.iterationCount = 10
    
    measure(metrics: [XCTClockMetric()], options: options) {
        sut.performOperation()
    }
}
```

## UI Testing Best Practices

### 1. Page Object Pattern
```swift
class LoginPage {
    let app: XCUIApplication
    
    init(app: XCUIApplication) {
        self.app = app
    }
    
    var emailField: XCUIElement {
        app.textFields["emailTextField"]
    }
    
    var passwordField: XCUIElement {
        app.secureTextFields["passwordTextField"]
    }
    
    var loginButton: XCUIElement {
        app.buttons["loginButton"]
    }
    
    func login(email: String, password: String) {
        emailField.tap()
        emailField.typeText(email)
        
        passwordField.tap()
        passwordField.typeText(password)
        
        loginButton.tap()
    }
}

// Usage in tests
func testLogin() {
    let loginPage = LoginPage(app: app)
    loginPage.login(email: "user@example.com", password: "password123")
    
    XCTAssertTrue(app.staticTexts["welcomeLabel"].exists)
}
```

### 2. Test Data Management
```swift
enum TestData {
    static let validEmail = "test@example.com"
    static let validPassword = "password123"
    static let invalidEmail = "invalid"
    
    static func createTestUser() -> User {
        User(id: UUID().uuidString, name: "Test User", email: validEmail)
    }
}
```

### 3. Launch Arguments
```swift
// In test
app.launchArguments = [
    "UI-Testing",
    "-MockData",
    "-DisableAnimations"
]
app.launch()

// In app
if CommandLine.arguments.contains("UI-Testing") {
    // Use mock data
}

if CommandLine.arguments.contains("-DisableAnimations") {
    UIView.setAnimationsEnabled(false)
}
```

## Common Pitfalls

### Pitfall 1: Not Cleaning Up
```swift
// ❌ Avoid - state leaks between tests
var sharedData: [String] = []

func testOne() {
    sharedData.append("test1")
}

// ✅ Clean up properly
override func tearDown() {
    sharedData.removeAll()
    super.tearDown()
}
```

### Pitfall 2: Flaky Tests
```swift
// ❌ Avoid - race conditions
func testFlaky() {
    sut.startAsyncOperation()
    XCTAssertTrue(sut.isComplete) // May fail
}

// ✅ Wait for completion
func testReliable() {
    let expectation = self.expectation(description: "Operation complete")
    sut.startAsyncOperation {
        expectation.fulfill()
    }
    waitForExpectations(timeout: 5.0)
    XCTAssertTrue(sut.isComplete)
}
```

### Pitfall 3: Testing Too Much
```swift
// ❌ Avoid - testing framework code
func testUIKitBehavior() {
    let button = UIButton()
    button.setTitle("Test", for: .normal)
    XCTAssertEqual(button.title(for: .normal), "Test")
}

// ✅ Test your code
func testButtonConfiguration() {
    sut.configureButton()
    XCTAssertEqual(sut.submitButton.title(for: .normal), "Submit")
    XCTAssertTrue(sut.submitButton.isEnabled)
}
```

## CI/CD Integration

### 1. Fastlane Configuration
```ruby
lane :test do
  scan(
    scheme: "YourApp",
    devices: ["iPhone 14", "iPhone 14 Pro"],
    clean: true,
    code_coverage: true
  )
end

lane :ui_test do
  scan(
    scheme: "YourApp",
    devices: ["iPhone 14"],
    only_testing: ["YourAppUITests"]
  )
end
```

### 2. GitHub Actions
```yaml
name: iOS Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: |
          xcodebuild test \
            -scheme YourApp \
            -destination 'platform=iOS Simulator,name=iPhone 14' \
            -enableCodeCoverage YES
```

## Essential Tools

- **XCTest**: Built-in testing framework
- **XCUITest**: UI testing framework
- **Quick/Nimble**: BDD-style testing
- **SnapshotTesting**: Visual regression testing
- **OHHTTPStubs**: Network request stubbing
- **Fastlane**: Automation and CI/CD
- **SwiftLint**: Code quality
- **Sourcery**: Code generation for mocks

## References
- [Apple Testing Documentation](https://developer.apple.com/documentation/xctest)
- [iOS Unit Testing Guide](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/testing_with_xcode/)
- [WWDC Testing Videos](https://developer.apple.com/videos/testing)

## Related Rules
- [React Native Best Practices](./react-native-best-practices.md)
- [Testing Strategies](../testing/testing-strategies.md)
- [Mobile App Security](../security-devops/mobile-security.md)
