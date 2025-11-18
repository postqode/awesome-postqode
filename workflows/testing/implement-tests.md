# Implement Tests Workflow

This workflow provides a structured process for converting an approved test plan into executable automated tests, regardless of the specific testing framework.

## Input

**Required:**
-   A detailed test plan, including scenarios, locators, and test data requirements.

**Optional:**
-   The specific scenarios to be implemented (if not all).
-   Any additional context or implementation notes.

## Workflow

### 1. Preparation and Environment Setup

-   **Review the Test Plan:** Thoroughly read the test plan to understand the scenarios, requirements, and existing components that can be reused.
-   **Validate Prerequisites:** Ensure that all necessary tools, libraries, and dependencies are installed and correctly configured.
-   **Prepare the Environment:** Set up any required test data, feature flags, or environment configurations as specified in the plan.

### 2. Implementation

For each scenario in the test plan:

-   **Create Test Structure:** Create the necessary test files and structure according to the project's conventions.
-   **Implement Test Code:**
    -   Write the test code, following the steps outlined in the test plan.
    -   Use the locators and test data specified in the plan.
    -   Implement assertions to verify the expected outcomes.
-   **Reuse Existing Components:** Leverage existing page objects, fixtures, and helper functions to avoid code duplication.
-   **Follow Best Practices:** Adhere to the project's coding standards, including naming conventions, formatting, and documentation.
-   **Implement Robust Waits:** Use explicit, dynamic waits instead of fixed delays to handle asynchronous operations and prevent flaky tests.

### 3. Refactoring and Cleanup

-   **Review and Refactor:** Once the initial implementation is complete, review the code for any opportunities to refactor and improve its quality.
-   **Remove Duplication:** Extract any duplicated code into reusable helper functions or fixtures.
-   **Ensure Readability:** Make sure the code is clean, well-documented, and easy to understand.

### 4. Verification and Validation

-   **Run Static Checks:** Run any linters or static analysis tools to check for code quality issues.
-   **Execute the Tests:** Run the newly implemented tests and ensure they pass consistently.
-   **Debug Failures:** If any tests fail, use debugging tools and logs to diagnose and fix the issues.
-   **Run a Regression Suite:** Execute a broader suite of tests to ensure that the new tests have not introduced any regressions.

### 5. Documentation and Handoff

-   **Summarize the Implementation:** Create a summary of the implemented scenarios, including the test file names and any new components that were created.
-   **Document Any Deviations:** Note any deviations from the original test plan and the reasons for them.
-   **Provide Execution Instructions:** Include the commands required to run the new tests.

## Best Practices

-   **Follow the Plan:** The test plan is the source of truth. Avoid deviating from it without a good reason and proper documentation.
-   **Don't Guess:** If the plan is missing critical information (e.g., locators, test data), ask for clarification rather than making assumptions.
-   **Fail Fast:** Configure aggressive timeouts to ensure that tests fail quickly when something goes wrong, providing rapid feedback.
-   **Write Maintainable Code:** Focus on creating tests that are not only correct but also easy to read, understand, and maintain over time.
