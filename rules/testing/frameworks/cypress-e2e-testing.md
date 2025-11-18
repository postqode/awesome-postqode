## Brief overview

This rule defines best practices for end-to-end testing with Cypress. It emphasizes reliable test automation, proper test organization, and comprehensive coverage strategies for web application testing.

## Test organization and structure

- Use Cypress's recommended folder structure (integration, fixtures, support)
- Organize tests by feature or page object model
- Create custom commands for reusable test actions
- Use page objects for element locators and interactions
- Implement proper test data management with fixtures
- Separate configuration files for different environments
- Use meaningful test descriptions and tags for categorization

## Selectors and element interaction

- Use data-testid attributes for reliable element selection
- Prefer Cypress's built-in selectors (get, contains, find)
- Implement proper waiting strategies for dynamic content
- Use role-based selectors for accessibility testing
- Avoid brittle selectors that depend on CSS classes or DOM structure
- Implement proper element visibility and interaction checks
- Use custom commands for complex interaction patterns

## Test writing best practices

- Write tests in Given-When-Then format for readability
- Use descriptive test names that explain the scenario
- Implement proper setup and teardown for each test
- Use beforeEach and afterEach hooks for test isolation
- Write atomic tests that focus on single user flows
- Implement proper assertions with explicit expectations
- Use custom assertions for domain-specific validations
- Implement proper error handling and test failure reporting

## Data management and fixtures

- Use fixtures for consistent test data across tests
- Implement factory functions for dynamic test data generation
- Use environment-specific configuration for different test scenarios
- Implement proper data cleanup between tests
- Use API mocking for isolated testing environments
- Create realistic test data that mirrors production scenarios
- Implement proper user session management in tests
- Use data seeding for complex test scenarios

## Network and API testing

- Use cy.intercept() for mocking API responses
- Implement proper request/response validation in tests
- Test network failures and error scenarios
- Use cy.wait() for API response timing
- Implement proper authentication handling in tests
- Test different network conditions (slow, offline)
- Use cy.request() for direct API testing when needed
- Implement proper CORS and security testing

## Visual and accessibility testing

- Use visual regression testing with screenshots
- Implement proper responsive design testing across viewports
- Test keyboard navigation and screen reader compatibility
- Use accessibility testing plugins and assertions
- Implement proper color contrast and visual hierarchy testing
- Test form validation and error messaging
- Use proper focus management and tab order testing

## Performance testing

- Use cy.tick() for testing time-based scenarios
- Implement proper performance metrics collection
- Test application load and response times
- Use memory profiling for long-running tests
- Implement proper animation and transition testing
- Test resource loading and optimization
- Use performance budgets for acceptable thresholds

## CI/CD integration

- Use Cypress Dashboard for test result visualization
- Implement proper parallel test execution for faster feedback
- Use environment-specific configuration for different stages
- Implement proper test reporting and artifact collection
- Use container-based execution for consistent environments
- Implement proper test flakiness detection and handling
- Use test result notifications and integration with project management

## Debugging and troubleshooting

- Use Cypress Studio for test creation and debugging
- Implement proper logging and console output in tests
- Use cy.debug() for step-by-step test execution
- Implement proper error message capture and analysis
- Use time-travel debugging for state inspection
- Implement proper test isolation for debugging specific scenarios
- Use network request inspection for API debugging

## Advanced testing patterns

- Implement custom commands for complex user interactions
- Use page object model for maintainable test suites
- Implement proper test data factories and builders
- Use behavior-driven development (BDD) patterns with Cucumber integration
- Implement proper cross-browser testing strategies
- Use visual testing for UI consistency verification
- Implement proper mobile and tablet testing scenarios

## Security testing

- Test authentication and authorization flows
- Implement proper input validation and sanitization testing
- Test for XSS and injection vulnerabilities
- Use security headers validation in tests
- Implement proper session management testing
- Test for CSRF and other security tokens
- Implement proper data encryption and privacy testing

## Test maintenance and optimization

- Regularly review and update test selectors
- Implement proper test refactoring for maintainability
- Use test analytics to identify flaky tests
- Implement proper test documentation and comments
- Regularly update dependencies and Cypress version
- Use test performance monitoring and optimization
- Implement proper test suite organization as application grows
