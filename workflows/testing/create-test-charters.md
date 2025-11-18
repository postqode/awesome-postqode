# Create Test Charters Workflow

This workflow guides the creation of effective, context-driven test charters by analyzing project requirements and risks.

> **IMPORTANT:** The goal is not to create a charter for every small task. Instead, this workflow helps identify areas that benefit most from focused, exploratory testing sessions.

## Input

**Required:**
- A clear description of the feature, user story, or area to be tested.

**Optional:**
- Additional context, such as architectural diagrams or user personas.
- Specific areas of focus or concern.
- The experience level of the testing team (e.g., Beginner, Intermediate, Advanced) to tailor the level of detail in the charters.

## Workflow

### 1. Gather Context

-   **Review Requirements:** Thoroughly understand the feature, its objectives, and acceptance criteria.
-   **Analyze Documentation:** Review any available documentation, mockups, or technical specifications.
-   **Identify Audience:** Determine the experience level of the testers to tailor the charter's level of detail.
    -   **Beginner:** Charters should include more detailed context and step-by-step guidance.
    -   **Intermediate:** Charters should provide a balance of guidance and room for exploration.
    -   **Advanced:** Charters can be more concise, focusing on high-risk areas and complex interactions.

### 2. Assess Charter Necessity

Before creating any charters, perform a critical evaluation to determine if they are needed.

#### Guiding Principles:

1.  **Complexity:**
    -   **Simple:** Minor UI changes or simple CRUD operations may not need a charter if covered by other tests.
    -   **Moderate:** New features with standard integrations may benefit from 1-2 focused charters.
    -   **Complex:** Features with complex business logic or multiple integration points may require 2-4 charters.

2.  **Risk:**
    -   **Low Risk:** Non-critical features with good automated test coverage may not need a charter.
    -   **Medium Risk:** Features on important user paths with partial automation may need 1-2 charters.
    -   **High Risk:** Critical features like payments, security, or data integrity will likely need multiple charters.

3.  **The 45-Minute Rule:**
    -   Each charter should be completable within a single, focused 45-minute testing session.
    -   If a topic takes less than 20 minutes, combine it with another.
    -   If it takes more than 45 minutes, split it into multiple, more focused charters.

4.  **Existing Coverage:**
    -   If automated tests (unit, integration, E2E) already provide sufficient coverage, a charter may be redundant.
    -   Charters are most valuable for exploring edge cases, complex interactions, and scenarios that are difficult to automate.

### 3. Propose a Charter Plan

Based on the necessity assessment, present a plan for user approval.

-   **Proposed Charters:** For each proposed charter, provide a title, a brief justification, and the risk it addresses.
-   **No Charters Proposed:** If no charters are needed, explain why (e.g., "This feature is low-risk and fully covered by our existing E2E test suite.").

Wait for user confirmation before proceeding.

### 4. Generate Test Charters

Once the plan is approved, generate the content for each test charter using the template below.

#### Test Charter Template

```markdown
# Test Charter: [Specific Testing Focus]

**Session Time Limit:** 45 minutes

## Mission
Explore [functionality or area] to discover [types of issues] that could impact [a stakeholder concern or user goal].

## Context
-   **Feature/Story:** [Brief description of the feature]
-   **Key Components:** [Relevant parts of the system]
-   **Documentation:** [Link to relevant documents, mockups, or specs]

## Justification
-   **Why This Charter is Needed:** [The specific risk or gap this charter addresses]
-   **What We're Looking For:** [Examples of potential defect types]
-   **Why Automation Isn't Enough:** [What automated tests might miss]

## Approach
-   **Testing Techniques:** [e.g., Scenario testing, exploratory testing, error guessing]
-   **Focus Areas:** [A prioritized list of areas to investigate within the 45-minute session]
-   **How to Determine Pass/Fail:** [The oracle or criteria for success]

## Test Ideas
-   [A few starting ideas to kick off the session]
-   [An edge case to consider]
-   [An integration point to check]

## Risks and Assumptions
-   **Risks:** [Any risks to the testing session itself]
-   **Assumptions:** [What is being assumed to be true]
-   **Dependencies:** [Any dependencies required for the session]

## Deliverables
-   Notes on test execution and observations.
-   Defect reports for any issues found.
-   A summary of the coverage achieved.
```

### 5. Final Summary

-   **Charters Created:** List the titles of the charters that were generated.
-   **Coverage Analysis:** Briefly describe the risks and areas covered by the new charters.
-   **Next Steps:** Provide recommendations for who should execute the charters and in what priority.
