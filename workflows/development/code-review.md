# Code Review Workflow

This workflow provides a structured, comprehensive checklist for conducting effective and consistent code reviews.

## Input

**Required:**
-   A pull request (PR) or merge request (MR) to be reviewed.

**Optional:**
-   Any specific areas of focus for the review.
-   The user story or ticket related to the changes.

## Workflow

### 1. Understand the Context

-   **Read the PR/MR Description:** Understand the purpose of the changes. What bug is being fixed or what feature is being implemented?
-   **Review the Related Ticket:** If a ticket is linked, review it to understand the full context and acceptance criteria.
-   **Check the Scope:** Does the scope of the changes match the scope of the ticket? Are there any unexpected changes?

### 2. High-Level Review

-   **Skim the Changes:** Get a high-level overview of the changes. How large and complex are they?
-   **Check the Architecture:** Do the changes fit within the existing architecture and design patterns of the project?
-   **Look for Major Issues:** Are there any obvious, major issues that would warrant an immediate rejection or request for major changes?

### 3. Detailed Code-Level Review

Go through the changes file by file, checking for the following:

#### Correctness
-   Does the code do what it's supposed to do?
-   Does it handle all edge cases and potential errors?
-   Is the logic sound?

#### Readability and Maintainability
-   Is the code easy to read and understand?
-   Are variable and function names clear and descriptive?
-   Is the code well-commented, especially in complex areas?
-   Is there any duplicated code that could be refactored into a reusable function?

#### Best Practices and Conventions
-   Does the code adhere to the project's established coding style and conventions?
-   Does it follow language-specific best practices?
-   Are there any security vulnerabilities (e.g., SQL injection, XSS)?

#### Testing
-   Are there new tests for the new functionality?
-   Do existing tests need to be updated?
-   Do all tests pass?
-   Is the test coverage sufficient?

#### Documentation
-   Has any relevant documentation (e.g., `README.md`, API docs) been updated?

### 4. Provide Feedback

-   **Be Constructive:** Frame your feedback in a positive and constructive way.
-   **Be Specific:** Clearly explain what the issue is, why it's an issue, and how it could be improved.
-   **Use a Conventional Commenting Structure:**
    -   **Praise:** Start with something positive.
    -   **Nitpick:** For minor, non-blocking issues, label them as "nitpicks."
    -   **Suggestion:** For improvements, offer a specific suggestion.
    -   **Question:** If you're unsure about something, ask a question.
    -   **Request for Change:** For issues that must be addressed, clearly state what needs to be changed.
-   **Batch Your Comments:** If possible, submit all your comments at once to avoid overwhelming the author with notifications.

### 5. Finalize the Review

-   **Summarize Your Feedback:** Provide a high-level summary of your review.
-   **Approve or Request Changes:**
    -   If the changes are good to go, approve the PR/MR.
    -   If there are issues that need to be addressed, request changes and clearly outline what is needed.
