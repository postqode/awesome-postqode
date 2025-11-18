# Fix Bug Workflow

This workflow provides a systematic, framework-agnostic process for investigating, fixing, and verifying bugs in any software project.

## Input

**Required:**
-   A clear description of the bug, including what happened, what was expected, and how to reproduce it.

**Optional:**
-   Screenshots, error logs, or stack traces.
-   Details about the environment where the bug occurred (e.g., browser version, OS, device).

## Workflow

### 1. Context and Understanding

-   **Review Project Documentation:** Read the project's `README.md` and any relevant architectural or feature documentation to understand the project's structure and conventions.
-   **Identify Key Files:** Based on the bug report, identify the most relevant parts of the codebase to investigate (e.g., specific components, services, or utility functions).
-   **Review Project Configuration:** Check configuration files (`package.json`, `pom.xml`, etc.) and linting rules to understand the project's dependencies and coding standards.

### 2. Bug Investigation

-   **Analyze the Bug Report:** Carefully examine all the information provided in the bug report to identify clues, such as error messages, UI anomalies, or specific user actions.
-   **Reproduce the Bug:** Follow the reproduction steps to reliably trigger the bug in a local development environment. If you can't reproduce it, you can't be sure you've fixed it.
-   **Trace the Code:** Use debugging tools, logs, and code analysis to trace the execution path and pinpoint the exact location of the issue.
-   **Identify the Root Cause:** Determine the underlying reason for the bug. Is it a logic error, a race condition, a type mismatch, or something else?

### 3. Propose a Fix

-   **Formulate a Solution:** Based on your root cause analysis, devise a clear plan to fix the bug.
-   **Consider Side Effects:** Think about any potential side effects or unintended consequences your fix might have on other parts of the application.
-   **Present Your Findings:** Before implementing the fix, present a summary of your findings to the user or team, including the root cause, the affected code, and your proposed solution.

### 4. Implementation

-   **Follow Project Conventions:** Adhere to the project's established coding style, patterns, and best practices.
-   **Write Clean Code:** Implement the fix in a clean, readable, and maintainable way.
-   **Update Related Files:** If the fix requires changes in multiple files (e.g., updating a type definition and the component that uses it), make sure all related changes are made.

### 5. Verification and Testing

-   **Run Linters and Quality Checks:** Run any configured linters or static analysis tools to ensure the new code meets the project's quality standards.
-   **Build the Project:** Ensure the project builds successfully without any new errors or warnings.
-   **Test the Fix:**
    -   Confirm that the original bug is no longer reproducible.
    -   Verify that the affected feature still works as expected.
-   **Regression Test:**
    -   Manually or automatically test related features to ensure your fix hasn't introduced any new bugs.
    -   Run the full test suite if one is available.

### 6. Documentation and Completion

-   **Document the Fix:** Add comments to the code to explain any complex parts of the fix. If necessary, update the project's documentation.
-   **Final Summary:** Provide a final summary of the work done, including a description of the bug, the solution, the files that were modified, and the results of your testing.

## Tips for Effective Bug Fixing

-   **Reproduce First:** Always confirm you can reproduce the bug before you start trying to fix it.
-   **Understand, Don't Just Guess:** Take the time to understand the root cause of the bug rather than just treating the symptoms.
-   **Make Small, Incremental Changes:** Avoid making large, sweeping changes that are difficult to test and review.
-   **Test Thoroughly:** Test your fix, test the surrounding functionality, and consider edge cases.
-   **Ask for Help:** If you're stuck, don't hesitate to ask a teammate for a second opinion.
