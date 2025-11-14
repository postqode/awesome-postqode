## Brief overview

This rule defines best practices for end-to-end testing with Playwright. It emphasizes reliable browser automation, proper test organization, and comprehensive coverage strategies for modern web application testing.

## Test organization and structure

- Use Playwright's recommended folder structure (tests, fixtures, pages)
- Organize tests by feature or page object model
- Create custom test fixtures and data factories
- Use page objects for element locators and interactions
- Implement proper test configuration with different browsers
- Separate configuration files for different environments
- Use meaningful test descriptions and tags for categorization
- Implement proper test utilities and helper functions

## Selectors and element interaction

- Use Playwright's built-in locators (page.locator(), getByRole(), getByText())
- Prefer semantic selectors over CSS selectors when possible
- Implement proper waiting strategies for dynamic content
- Use data-testid attributes for reliable element selection
- Use role-based selectors for accessibility testing
- Avoid brittle selectors that depend on DOM structure
- Implement proper element visibility and interaction checks
- Use custom locators for complex element selection
- Implement proper frame and iframe handling

## Test writing best practices

- Write tests using test() and expect() patterns
- Use descriptive test names that explain the scenario
- Implement proper setup and teardown for each test
- Use test.step() for better test organization and reporting
- Write atomic tests that focus on single user flows
- Implement proper assertions with explicit expectations
- Use soft assertions for non-critical validations
- Implement proper error handling and test failure reporting
- Use test hooks for setup, teardown, and custom logic

## Browser and device testing

- Test across multiple browsers (Chromium, Firefox, WebKit)
- Implement proper device emulation for mobile testing
- Use viewport configuration for responsive design testing
- Test different network conditions (slow, offline)
- Implement proper browser context management
- Use browser-specific features and APIs when needed
- Test geolocation and permission APIs
- Implement proper browser storage and cookie testing

## API and network testing

- Use page.route() for mocking API responses
- Implement proper request/response interception and modification
- Test network failures and error scenarios
- Use page.waitForResponse() for API timing validation
- Implement proper authentication and authorization testing
- Test different HTTP methods and status codes
- Use page.waitForLoadState() for page load verification
- Implement proper WebSocket and real-time communication testing

## Visual and accessibility testing

- Use page.screenshot() for visual regression testing
- Implement proper visual comparison and diffing
- Test accessibility with page.accessibility.snapshot()
- Use proper color contrast and visual hierarchy testing
- Test keyboard navigation and screen reader compatibility
- Implement proper focus management and tab order testing
- Use accessibility testing tools and assertions
- Test form validation and error messaging accessibility

## Performance testing

- Use page.waitForLoadState() for performance measurement
- Implement proper performance metrics collection
- Test application load and response times
- Use browser developer tools integration
- Implement proper memory and resource monitoring
- Test animation and transition performance
- Use performance budgets and thresholds
- Implement proper profiling and optimization strategies

## Data management and fixtures

- Use test fixtures for consistent test data
- Implement data factories for dynamic test data generation
- Use environment-specific configuration for different test scenarios
- Implement proper data cleanup between tests
- Use API mocking for isolated testing environments
- Create realistic test data that mirrors production scenarios
- Implement proper user session and authentication testing
- Use data seeding for complex test scenarios

## CI/CD integration

- Use Playwright's CI integration with proper configuration
- Implement proper parallel test execution for faster feedback
- Use environment-specific configurations for different stages
- Implement proper test reporting and artifact collection
- Use container-based execution for consistent environments
- Implement proper test flakiness detection and handling
- Use test result notifications and integration with project management
- Configure proper test retries and timeout handling

## Advanced testing patterns

- Implement custom page object models for complex applications
- Use behavior-driven development (BDD) patterns with Cucumber integration
- Implement proper cross-browser testing strategies
- Use visual testing for UI consistency verification
- Implement proper mobile and tablet testing scenarios
- Use network simulation for different connection conditions
- Implement proper component testing patterns
- Use API testing for backend integration validation

## Debugging and troubleshooting

- Use Playwright Inspector for step-by-step test execution
- Implement proper logging and console output in tests
- Use page.pause() for interactive debugging
- Implement proper trace collection and analysis
- Use browser developer tools integration
- Implement proper error message capture and analysis
- Use time-travel debugging for state inspection
- Implement proper test isolation for debugging specific scenarios

## Security testing

- Test authentication and authorization flows
- Implement proper input validation and sanitization testing
- Test for XSS and injection vulnerabilities
- Use security headers validation in tests
- Implement proper session management testing
- Test for CSRF and other security tokens
- Implement proper data encryption and privacy testing
- Use proper HTTPS and secure communication testing

## Test maintenance and optimization

- Regularly review and update test selectors
- Implement proper test refactoring for maintainability
- Use test analytics to identify flaky tests
- Implement proper test documentation and comments
- Regularly update dependencies and Playwright version
- Use test performance monitoring and optimization
- Implement proper test suite organization as application grows
- Use proper test data management and cleanup strategies
