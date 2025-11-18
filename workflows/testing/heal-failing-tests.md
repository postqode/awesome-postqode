# Heal Failing Tests Workflow

This workflow provides a systematic process for diagnosing and fixing failing automation tests in a framework-agnostic way.

## Input

**Required:**
-   A list of failing test identifiers (e.g., file paths, test names, or IDs).

**Optional:**
-   Error logs or stack traces.
-   Information about recent changes to the application or test suite.
-   The specific test charter or user story related to the failing tests.

## Workflow

### 1. Discovery and Context

-   **Detect Framework:** Identify the testing framework and language from project rules or configuration files.
-   **Analyze Test Structure:** Read the failing test files to understand their structure, dependencies, and any abstraction layers being used (e.g., Page Object Model).
-   **Review Related Artifacts:** If provided, review any related user stories, test charters, or recent code changes that might provide context for the failure.

### 2. Reproduce and Diagnose

-   **Execute and Observe:** Run the failing tests to reproduce the failure.
-   **Collect Diagnostics:** Capture all relevant diagnostic information, such as error messages, stack traces, screenshots, and videos.
-   **Determine Flakiness:** Run the tests multiple times (e.g., 3-5 times) to determine if the failure is consistent or intermittent (flaky).

### 3. Root Cause Analysis

Systematically investigate the most common causes of test failures:

1.  **Locator/Selector Issues (for UI tests):**
    -   Have element locators (e.g., IDs, CSS selectors, XPath) changed?
    -   Is the element visible and interactable when the test tries to access it?

2.  **Timing and Synchronization:**
    -   Is the test failing because it's not waiting for an asynchronous operation to complete?
    -   Are there missing or inadequate waits for elements to appear or become stable?

3.  **Test Data Issues:**
    -   Is the test data correct and available?
    -   Is there data pollution from a previous test?
    -   Are setup and teardown procedures working as expected?

4.  **Assertion Failures:**
    -   Has the application's behavior changed, causing a mismatch between the expected and actual results?
    -   Is the correct assertion method being used?

5.  **Application Changes:**
    -   Have there been recent changes to the UI, API, or business logic that would affect the test?

6.  **Environment Issues:**
    -   Are there differences in configuration or versions between the local and CI/CD environments?

### 4. Remediate

-   **Apply Fixes:** Apply the necessary fixes based on the root cause.
    -   Update locators to be more stable and semantic.
    -   Add or improve explicit waits.
    -   Correct test data or improve setup/teardown logic.
    -   Update assertions to match the new application behavior.
-   **Follow Best Practices:** Adhere to the project's coding standards and the testing framework's best practices.
-   **Document Changes:** Add comments to the code explaining the fix.

### 5. Verify

-   **Confirm the Fix:** Run the fixed tests multiple times (e.g., 5 times) to ensure the fix is stable and the test passes consistently.
-   **Check for Side Effects:** Run the entire test suite or a related subset of tests to ensure the fix has not introduced any new failures.
-   **Run Quality Checks:** Run any code quality checks, such as linting or formatting.

### 6. Document and Communicate

-   **Summarize the Fix:** Create a summary of the work done, including the root cause of the failure and the solution that was implemented.
-   **Update Tracking Systems:** If the failure was tracked in a project management tool, update the ticket with the resolution.
-   **Share Lessons Learned:** If the failure revealed a recurring problem, share the lessons learned with the team to prevent similar issues in the future.
