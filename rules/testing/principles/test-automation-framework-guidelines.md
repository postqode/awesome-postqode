## Brief Overview

This rule defines generic test automation framework guidelines applicable to any project. The focus is on maintainability, readability, and scalability, regardless of the specific technology stack.

## Technology Stack Principles

- Choose a primary test automation framework that fits the project's needs.
- Select libraries for UI, API, and database testing that integrate well with the chosen framework.
- Use a programming language that the team is proficient in for writing custom logic and utilities.
- Employ common design patterns like the Page Object Model (POM) where applicable.
- Favor a data-driven approach to separate test logic from test data.

## Project Structure

- Organize tests in a clear hierarchy (e.g., `tests/ui/`, `tests/api/`).
- Store reusable components like page objects or screen objects in a dedicated directory (e.g., `tests/pages/`).
- Keep reusable functions or keywords in a shared directory (e.g., `tests/keywords/` or `tests/helpers/`).
- Manage test data in a separate directory (e.g., `tests/data/`).
- Place configuration files in their own directory (e.g., `tests/config/`).
- Store locators, variables, and other resources in a `tests/resources/` directory.
- Exclude test reports and logs from version control.

## Naming Conventions

- **Test Files:** Use descriptive names that reflect the functionality being tested (e.g., `test_login_functionality.js`, `user_registration_spec.py`).
- **Test Cases:** Clearly describe the test's purpose (e.g., `should login successfully with valid credentials`).
- **Functions/Keywords:** Use action-oriented names (e.g., `enterUsernameAndPassword`, `verifyDashboardIsDisplayed`).
- **Page/Screen Objects:** Name files after the page or component they represent (e.g., `login_page.js`, `dashboard_screen.py`).
- **Variables:** Use clear, uppercase names for constants and descriptive names for other variables (e.g., `USERNAME`, `EXPECTED_TITLE`).

## Page Object Model (POM) or Screen Object Model

- Create separate object files for each application page, screen, or major component.
- Define element locators as variables within these files.
- Implement page-specific functions that encapsulate interactions.
- Keep business logic out of page objects; they should only interact with the UI.
- Use descriptive names for locators (e.g., `LOGIN_BUTTON`, `USERNAME_INPUT`).

## Locator Strategy

- Prioritize locators in the following order:
  1. User-facing attributes (e.g., accessibility roles, labels, text).
  2. Stable test IDs (e.g., `data-testid`).
  3. CSS selectors or other query methods as a last resort.
- Avoid brittle locators like absolute XPath or dynamically generated class names.
- Store all locators as variables in page/screen objects, not hardcoded in test steps.

## Wait Strategies for UI Testing

- Always use explicit waits; never use fixed sleeps or delays.
- Leverage the built-in wait mechanisms of your chosen framework (e.g., waiting for an element to be visible, clickable, or stable).
- Wait for page load states or network activity to settle before proceeding.
- Set appropriate timeouts based on the application's expected performance.

## Setup and Teardown

- Use suite-level setup/teardown for one-time initialization and cleanup (e.g., launching a browser, setting up a database connection).
- Use test-level setup/teardown for actions that need to run before and after each test (e.g., logging in, clearing state).
- Ensure teardown actions run even if a test fails.
- Capture screenshots or other diagnostic information on failure.

## Data-Driven Testing

- Store test data in external files (e.g., CSV, JSON, YAML).
- Use framework features for parameterizing tests with data from these files.
- Separate test data from test logic to improve maintainability.

## API Testing Best Practices

- Validate response status codes, headers, and bodies.
- Use JSON schema validation to check response structures.
- Store API endpoints and base URLs as variables in a configuration file.
- Create reusable functions for common API operations (e.g., GET, POST).
- Log request and response details for easier debugging.

## Database Testing Best Practices

- Always close database connections in a teardown block.
- Use parameterized queries to prevent SQL injection.
- Validate data integrity before and after test operations.
- Implement database cleanup procedures to ensure test isolation.

## General Code Best Practices

- Follow the established style guide for your chosen programming language (e.g., PEP 8 for Python, ESLint rules for JavaScript).
- Use type hints or annotations if your language supports them.
- Implement robust error handling.
- Write clear docstrings or comments for functions and modules.
- Keep functions small and focused on a single purpose.
- Use virtual environments or package managers to handle dependencies.

## Test Case Design

- Each test case should verify a single, specific piece of functionality.
- Use a descriptive name that clearly states the test's intent.
- Structure tests logically, such as with a Given-When-Then or Arrange-Act-Assert pattern.
- Keep test cases independent and self-contained.
- Use tags to categorize tests (e.g., `smoke`, `regression`, `ui`).

## Reporting and Logging

- Utilize the reporting features of your test framework.
- Implement custom logging for important test steps and state changes.
- Capture screenshots and other artifacts on test failure.
- Log API requests and responses for debugging.
- Generate easy-to-read HTML or console reports.

## Version Control and Collaboration

- Write meaningful commit messages.
- Use feature branches for developing new tests.
- Conduct code reviews for test code.
- Keep non-sensitive test data in version control.
- Document the test framework setup and contribution process in a `README.md` file.
