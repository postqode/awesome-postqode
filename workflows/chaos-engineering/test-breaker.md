# Test Breaker Workflow

This workflow provides a framework for intentionally and systematically introducing controlled failures into an existing automated test suite. The purpose is to simulate real-world scenarios that cause test breakage, thereby testing the resilience of the suite and the effectiveness of any "healing" or diagnostic processes.

## Purpose

-   Create authentic test failure scenarios to validate the robustness of your testing framework and processes.
-   Train team members on how to diagnose and fix common test failures.
-   Provide a controlled environment for demonstrating and testing automated test-healing capabilities.

## Input

**Required:**
-   A trigger command to initiate the process.

**Optional:**
-   `failure_types`: A list of specific failure types to introduce (e.g., `locator`, `timing`, `assertion`). Defaults to a mix of common failure types.
-   `severity`: The extent of the breakage (e.g., `minor`, `moderate`, `severe`). Defaults to `moderate`.
-   `test_scope`: Specific test files or scenarios to target. Defaults to a representative sample of the test suite.
-   `preserve_backup`: A boolean indicating whether to create backups of the original test files before introducing failures. Defaults to `false`.

## Workflow

### 1. Preparation and Discovery

-   **Scan the Test Suite:** Identify all test files, page objects (or other UI abstractions), and any test fixtures or setup files.
-   **Establish a Baseline:** Run the test suite to ensure all tests are currently passing. This baseline is crucial for verifying that the introduced failures are the only cause of subsequent test failures.
-   **Create Backups (if requested):** If `preserve_backup` is true, create a backup of the test suite in a separate directory before making any changes.

### 2. Select Failure Scenarios

Based on the `failure_types` input or a default mix, choose from a list of realistic failure scenarios.

#### Common Failure Scenarios:

1.  **Locator Changes (for UI tests):**
    -   **Scenario:** A developer has changed element IDs, `data-testid` attributes, or CSS classes.
    -   **Implementation:** Modify locators in the test code to no longer match the application's front end.

2.  **UI Text Changes:**
    -   **Scenario:** A copywriter or developer has updated the text of a button, link, or header.
    -   **Implementation:** Change the expected text in text-based locators or assertions.

3.  **Timing and Synchronization Issues:**
    -   **Scenario:** A new asynchronous operation has been introduced, or an existing one has become slower.
    -   **Implementation:** Remove explicit waits, or introduce actions that require waiting for dynamic content to load.

4.  **Form and Validation Changes:**
    -   **Scenario:** A form's structure or validation rules have been modified.
    -   **Implementation:** Change the name of a form field, add a new required field, or alter a validation rule in the test.

5.  **Navigation and Routing Changes:**
    -   **Scenario:** The application's URL structure or navigation flow has been updated.
    -   **Implementation:** Change a URL in a `goto` command or modify a step in a navigation sequence.

6.  **Assertion Failures:**
    -   **Scenario:** The underlying business logic has changed, leading to different results.
    -   **Implementation:** Change the expected value in an assertion to something that will not match the actual result.

### 3. Introduce Failures

-   Systematically modify the test files to introduce the selected failures.
-   Distribute the failures across different tests and files to create a realistic and varied set of challenges.
-   Ensure that the introduced failures are logical and reflect real-world issues, rather than just creating syntax errors.

### 4. Verify the Breakage

-   **Run the Tests:** Execute the modified test suite and confirm that the intended tests fail.
-   **Validate the Failures:** Check that the error messages are realistic and provide enough information for a developer or a "healer" workflow to diagnose the issue.
-   **Document the Results:** Create a report that lists the introduced failures, the affected tests, and the resulting error messages.

## Best Practices

-   **Use Version Control:** In a real-world scenario, always use a version control system like Git to manage changes. Create a new branch for the "broken" tests so you can easily revert to the original state.
-   **Be Realistic:** The goal is to simulate real-world problems, not to create unsolvable puzzles.
-   **Document Everything:** Keep a clear record of what was changed, where, and why. This is essential for using this workflow as a training tool.
-   **Start Small:** Begin by introducing a few simple failures and gradually increase the complexity as your team's diagnostic skills improve.
