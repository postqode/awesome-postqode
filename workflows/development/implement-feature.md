# Implement Feature Workflow

This workflow provides a structured, framework-agnostic process for implementing a new feature, from understanding the requirements to final verification.

## Input

**Required:**
-   A clear description of the feature to be implemented, such as a user story, a technical specification, or a requirements document.

**Optional:**
-   UI/UX mockups or design files.
-   Architectural diagrams.
-   Related documentation or context.

## Workflow

### 1. Understand the Requirements

-   **Review All Documentation:** Thoroughly read the feature specification, user story, and any related documents to fully understand the goals, scope, and acceptance criteria.
-   **Analyze the Existing Codebase:** Identify the parts of the codebase that will be affected by the new feature.
-   **Ask Clarifying Questions:** If any part of the requirements is unclear, ask for clarification before starting implementation.

### 2. Plan the Implementation

-   **Break Down the Feature:** Decompose the feature into smaller, manageable tasks (e.g., create a new API endpoint, build a new UI component, update the database schema).
-   **Identify Files to Modify:** List the files that will need to be created or modified.
-   **Propose a Plan:** Present a high-level implementation plan, including the proposed changes and any new dependencies, for feedback and approval.

### 3. Implementation

-   **Follow Project Conventions:** Adhere to the project's established coding style, patterns, and best practices.
-   **Write Clean, Maintainable Code:** Focus on writing code that is easy to read, understand, and maintain.
-   **Create or Modify Files:** Implement the changes as outlined in the plan.

### 4. Write and Update Tests

-   **Unit Tests:** Write unit tests for any new functions, methods, or classes.
-   **Integration Tests:** Add integration tests to verify that the new feature works correctly with other parts of the system.
-   **End-to-End Tests:** Create or update E2E tests to cover the new user flows.
-   **Ensure Coverage:** Aim for a level of test coverage that is consistent with the project's standards.

### 5. Verification and Validation

-   **Run All Tests:** Execute the entire test suite to ensure that the new feature works and has not introduced any regressions.
-   **Run Linters and Quality Checks:** Use static analysis tools to check for code quality issues.
-   **Manual Verification:** Manually test the feature to ensure it meets all requirements and provides a good user experience.

### 6. Update Documentation

-   **Code Comments:** Add comments to explain any complex or non-obvious parts of the code.
-   **READMEs and Wikis:** Update any relevant `README.md` files, API documentation, or wikis to reflect the new feature.

### 7. Final Review and Completion

-   **Summarize the Work:** Create a summary of the implementation, including the files that were changed and the new functionality that was added.
-   **Prepare for Code Review:** Ensure the code is ready for a code review by cleaning it up, adding necessary documentation, and providing a clear description of the changes.
