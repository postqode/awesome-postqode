# Create Automation Tests Workflow

This workflow guides the creation of strategic end-to-end automation tests by analyzing requirements and identifying high-value, repeatable scenarios worth automating.

> **IMPORTANT:** This workflow does not aim to convert every requirement into an automated test. Instead, it focuses on synthesizing insights to identify critical, repeatable end-to-end workflows that provide the maximum return on investment (ROI) when automated.

> **FRAMEWORK AGNOSTIC:** This workflow adapts to your project's testing framework. Framework details are detected from project rules, configuration files, or requested from the user if not found.

## Input

**Required:** A clear description of the feature or user story to be tested.

**Optional:**
- The testing framework to be used (if not auto-detected).
- Additional context or specific scenarios to prioritize.
- Browser or environment preferences.

## Workflow

### 1. Gather Context

- **Review Requirements:** Understand the feature, its goals, and acceptance criteria.
- **Analyze Existing Documentation:** Check for any existing documentation, diagrams, or mockups that provide context.
- **Detect Testing Framework:**
  - Check for project-specific test framework rules or configuration files.
  - If not found, auto-detect from the project structure and dependencies.
  - If the framework cannot be detected, ask the user to specify it.

### 2. Assess Automation Suitability

Perform a thorough evaluation of the feature to determine if it is a good candidate for automation.

#### Rejection Criteria (Stop if any apply):

1.  **No Repeatable Workflows:** The feature is for one-off or exploratory tasks with no repeatable user journeys.
2.  **Unstable or Incomplete Feature:** The feature is still in active development, or its requirements are changing frequently.
3.  **Visual/UX Validation Focus:** The primary testing goal is to validate visual design, layout, or user experience, which requires human judgment.
4.  **Low Business Value:** The feature is rarely used or not critical to the business, making the ROI of automation low.
5.  **Highly Variable Scenarios:** The feature involves scenarios with unpredictable inputs or context-dependent outcomes that are difficult to automate reliably.

If any of these criteria are met, the feature is not a good candidate for automation at this time.

#### Proceed Criteria (Must meet all):

1.  **Repeatable Workflows:** The feature includes clear, consistent user journeys that will be executed regularly.
2.  **Stable Feature:** The feature is complete and stable enough for automation.
3.  **Business Critical:** The feature involves high-value workflows that justify the investment in automation.
4.  **Clear E2E Paths:** The feature is part of identifiable end-to-end workflows that span multiple components.
5.  **Deterministic Outcomes:** The feature produces predictable results that can be reliably verified.

### 3. Propose a Test Plan

If the feature is a good candidate for automation, present a clear test plan.

- **Automation Suitability:** Justify why the feature is worth automating.
- **Testing Framework:** Specify the detected or chosen framework, language, and test type (e.g., E2E, API).
- **Proposed Test Structure:** Outline the proposed test files, abstraction layers (e.g., Page Object Model), and test data organization.
- **Automation Strategy:**
  - List high-priority end-to-end scenarios to be automated.
  - List any scenarios that will be explicitly excluded from automation and explain why.
- **ROI Justification:** Briefly explain the expected ROI in terms of execution frequency, time saved, and risk coverage.

Wait for user confirmation before proceeding.

### 4. Create Test Infrastructure

- **Configuration:** Create or update framework and environment configuration files.
- **Abstraction Layer:** Implement page objects, component objects, or API clients according to the project's established patterns.
- **Test Data:** Create and organize test data files, ensuring no sensitive data is hardcoded.
- **Setup/Teardown:** Implement setup and teardown mechanisms using framework-specific fixtures or hooks.

### 5. Create Test Files

- **Follow Conventions:** Adhere to the framework's conventions and the project's established patterns.
- **Descriptive Naming:** Use clear, descriptive names for test files and test cases.
- **Arrange-Act-Assert:** Structure tests using a clear pattern like Arrange-Act-Assert.
- **Independence:** Ensure tests are independent and can be run in any order.
- **Use Abstractions:** Use the abstraction layer for all interactions; avoid direct UI or API calls in tests.

### 6. Run and Fix Tests

- **Execute Tests:** Run the tests using the appropriate command for the framework.
- **Debug Failures:** If tests fail, review the error messages, check locators, timing, and logic, and use the framework's debugging tools to fix the issues.

### 7. Final Summary

- **Test Files Created:** List the new test files and the number of tests in each.
- **Abstractions Created:** List the new abstraction layer files.
- **Test Data Files:** List the new test data files.
- **Automation Coverage:** Summarize the automation coverage, including the number of workflows automated and the estimated ROI.
- **Test Results:** Provide a summary of the test run, including the number of passed and failed tests.
- **Running Tests:** Include the command to run the newly created tests.

## Automation Philosophy

-   **Strategic Synthesis:** Do not convert every requirement into a test. Focus on synthesizing requirements into strategic, end-to-end business workflows.
-   **Value-Driven Automation:** Automate only repeatable, high-value scenarios. Leave exploratory, visual, and judgment-based testing to manual efforts.
-   **Quality over Quantity:** Aim for a small number of robust tests rather than a large number of brittle ones.
-   **Reject Unsuitable Candidates:** Be prepared to reject automation requests that do not meet the criteria for providing a clear ROI.
