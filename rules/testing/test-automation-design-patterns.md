## Brief overview

This rule defines comprehensive design patterns for test automation across different frameworks and technologies. It emphasizes Page Object Model (POM), data-driven testing, and modern locator strategies for building maintainable and scalable test suites.

## Page Object Model (POM) patterns

### Core POM principles
- Separate page object classes from test logic for maintainability
- Implement proper inheritance with base page classes for common functionality
- Use proper encapsulation of page elements and interactions
- Design page objects with single responsibility principle
- Implement proper element locators with semantic selectors
- Use proper page object composition and delegation patterns
- Implement proper page object initialization and cleanup

### Base page class structure
```typescript
class BasePage {
  constructor(protected page: Page) {
    this.page = page;
    this.timeout = 30000; // Default timeout
  }

  async waitForElement(selector: string, timeout?: number): Promise<ElementHandle> {
    return await this.page.waitForSelector(selector, { timeout: timeout || this.timeout });
  }

  async waitForElements(selector: string, timeout?: number): Promise<ElementHandle[]> {
    return await this.page.waitForSelector(selector, { timeout: timeout || this.timeout });
  }

  async clickElement(selector: string, timeout?: number): Promise<void> {
    const element = await this.waitForElement(selector, timeout);
    await element.click();
  }

  async typeText(selector: string, text: string, timeout?: number): Promise<void> {
    const element = await this.waitForElement(selector, timeout);
    await element.fill(text);
  }

  async getElementText(selector: string, timeout?: number): Promise<string> {
    const element = await this.waitForElement(selector, timeout);
    return await element.textContent();
  }

  async navigateTo(url: string): Promise<void> {
    await this.page.goto(url, { waitUntil: 'domcontentloaded' });
  }

  async takeScreenshot(path?: string): Promise<string> {
    return await this.page.screenshot({ path: path, fullPage: true });
  }
}
```

### Specialized page objects
```typescript
class LoginPage extends BasePage {
  private readonly usernameInput = '#username';
  private readonly passwordInput = '#password';
  private readonly submitButton = '#submit-button';
  private readonly errorMessage = '#error-message';

  async login(username: string, password: string): Promise<void> {
    await this.typeText(this.usernameInput, username);
    await this.typeText(this.passwordInput, password);
    await this.clickElement(this.submitButton);
  }

  async getErrorMessage(): Promise<string | null> {
    try {
      return await this.getElementText(this.errorMessage);
    } catch {
      return null;
    }
  }

  async isLoggedIn(): Promise<boolean> {
    const errorElement = await this.page.$(this.errorMessage);
    return errorElement === null;
  }
}
```

## Data-driven testing patterns

### Test data management
- Use factory pattern for creating test data objects
- Implement builder pattern for complex test data creation
- Use fixtures for static test data with proper versioning
- Create data providers for different test scenarios and environments
- Implement proper data cleanup and isolation between tests
- Use faker or similar libraries for realistic test data generation
- Implement proper data validation and type safety for test data

### Data-driven test structure
```typescript
interface TestData {
  username: string;
  password: string;
  email: string;
  role: 'admin' | 'user' | 'guest';
}

class DataFactory {
  static createUser(overrides?: Partial<TestData>): TestData {
    return {
      username: overrides?.username || faker.internet.userName(),
      password: overrides?.password || faker.internet.password(),
      email: overrides?.email || faker.internet.email(),
      role: overrides?.role || 'user'
    };
  }

  static createAdminUser(): TestData {
    return this.createUser({ role: 'admin' });
  }
}
```

## Modern locator strategies

### Playwright locator best practices
- Use semantic locators (getByRole, getByLabel, getByPlaceholder) over CSS selectors
- Implement proper fallback strategies for dynamic elements
- Use data-testid attributes for reliable element identification
- Chain locators for complex element selection (filter, locator)
- Use proper waiting strategies with waitFor and expect
- Implement proper frame and iframe handling with contentFrame
- Use proper shadow DOM piercing techniques when needed

### Cross-framework locator patterns
```typescript
// Playwright example
class WebAppPage {
  constructor(private page: Page) {
    this.page = page;
  }

  // Semantic locator
  getSubmitButton() {
    return this.page.getByRole('button', { name: 'Submit' });
  }

  // Data-testid locator
  getModal() {
    return this.page.getByTestId('user-modal');
  }

  // Chained locator with filtering
  getActiveMenuItems() {
    return this.page.locator('.menu-item').filter({ hasText: 'Active' });
  }

  // Label-based locator
  getSearchInput() {
    return this.page.getByLabel('Search');
  }

  // Placeholder-based locator
  getEmailField() {
    return this.page.getByPlaceholder('Enter your email');
  }
}
```

### Cypress locator patterns
```typescript
// Cypress example
class WebAppPage {
  constructor() {
    // Cypress automatically exposes cy object
  }

  // Semantic locator
  getSubmitButton() {
    return cy.get('button[type="submit"]');
  }

  // Data-testid locator
  getModal() {
    return cy.get('[data-testid="user-modal"]');
  }

  // Contains text locator
  getErrorMessage() {
    return cy.contains('Invalid credentials');
  }

  // Custom command
  login(username: string, password: string) {
    cy.get('#username').type(username);
    cy.get('#password').type(password);
    cy.get('#submit').click();
  }
}
```

## Test automation architecture patterns

### Test suite organization
- Implement proper test hierarchy with base test classes
- Use composition over inheritance for test functionality
- Implement proper test configuration and setup management
- Use proper test data management and cleanup strategies
- Implement proper reporting and result aggregation
- Use proper parallel test execution and resource management

### Configuration management
- Implement environment-specific test configurations
- Use proper test settings and timeout management
- Implement proper browser and device configuration
- Use proper credential and security management for tests
- Implement proper test data versioning and environment switching

### Reporting and analytics
- Implement proper test result reporting and visualization
- Use proper test metrics collection and analysis
- Implement proper test failure documentation and debugging
- Use proper test trend analysis and quality metrics
- Implement proper integration with CI/CD pipelines and test management systems

## Framework-specific patterns

### Playwright testing patterns
- Use proper page object model with Playwright's Page class
- Implement proper test context management with test.fixtures()
- Use proper browser context isolation with test.browser.newContext()
- Implement proper network interception and mocking with page.route()
- Use proper API testing with page.waitForResponse()
- Implement proper visual testing with page.screenshot() and expect()

### Cypress testing patterns
- Use proper custom commands for reusable test actions
- Implement proper page object model with Cypress support classes
- Use proper alias management for element references
- Implement proper network stubbing with cy.intercept()
- Use proper fixture management with cy.fixture()
- Implement proper test data seeding and cleanup

### Selenium WebDriver patterns
- Use proper WebDriverWait for element waiting
- Implement proper explicit waits over implicit waits
- Use proper By locators with semantic selectors
- Implement proper JavascriptExecutor for advanced interactions
- Use proper Actions class for complex user interactions
- Implement proper expected conditions with WebDriverWait

## Advanced testing patterns

### Behavior-driven development (BDD)
- Implement proper Gherkin feature file organization
- Use proper step definition and parameterization
- Implement proper scenario outline and test data management
- Use proper test execution with cucumber-js or similar frameworks
- Implement proper reporting and documentation for BDD tests

### Visual regression testing
- Implement proper screenshot comparison and diffing
- Use proper visual baseline management and versioning
- Implement proper cross-browser visual testing strategies
- Use proper responsive design testing across different viewports
- Implement proper visual accessibility testing with automated tools

### Performance testing patterns
- Implement proper load testing with concurrent user simulation
- Use proper performance metrics collection and analysis
- Implement proper memory and resource monitoring in tests
- Use proper test execution time measurement and optimization
- Implement proper database performance testing with realistic data volumes

### API testing patterns
- Implement proper contract testing with schema validation
- Use proper API mocking and virtualization strategies
- Implement proper load testing and stress testing
- Use proper API versioning and backward compatibility testing
- Implement proper security testing with authentication and authorization

## Test data management strategies

### Environment-specific test data
- Use proper test data factories for different environments
- Implement proper test data versioning and migration
- Use proper sensitive data handling and masking
- Implement proper test data cleanup and restoration
- Use proper test data isolation and independence

### Test data generation
- Use realistic test data that mirrors production patterns
- Implement proper edge case and boundary condition testing
- Use proper randomization for unique test data
- Implement proper relationship and constraint testing
- Use proper performance testing data with realistic volumes

## Test maintenance and optimization

### Test suite organization
- Implement proper test refactoring and code cleanup
- Use proper test documentation and knowledge sharing
- Implement proper test review and quality assurance processes
- Use proper test deprecation and migration strategies
- Implement proper test performance monitoring and optimization

### Continuous integration
- Implement proper test automation in CI/CD pipelines
- Use proper test result reporting and notification
- Implement proper test environment provisioning and cleanup
- Use proper test parallelization and resource optimization
- Implement proper test quality gates and deployment criteria

## Best practices summary

- Design tests for maintainability and readability
- Implement proper error handling and debugging strategies
- Use proper test isolation and independence
- Implement proper data management and cleanup
- Use appropriate mocking and test double patterns
- Design tests for reliability and repeatability
- Implement proper performance and scalability considerations
- Use proper documentation and knowledge sharing
- Regularly review and refactor test code for quality
