# Plan E2E Tests Workflow

This workflow provides a structured, framework-agnostic process for analyzing end-to-end test scenarios and creating a clear, actionable implementation plan.

## Input

**Required:**
-   A detailed description of the end-to-end scenario to be tested, either as a document or a step-by-step description.

**Optional:**
-   The testing framework to be used (if not easily auto-detected).
-   Any existing test framework documentation or conventions.

## Workflow

### 1. Analyze the Scenario

-   **Identify Systems:** List all the systems, applications, or services involved in the scenario.
-   **Identify Actions:** Note all the key actions performed, such as "create," "sync," "validate," "update," or "delete."
-   **Identify Data Entities:** Identify the core data entities being manipulated, such as "customer," "order," or "product."
-   **Map the Flow:** Outline the sequence of actions and the direction of data flow between systems.
-   **Extract Key Details:** Note any specific navigation paths, UI elements (buttons, forms, fields), or API calls mentioned in the scenario.

### 2. Analyze the Existing Framework

-   **Review Existing Components:** Check for any reusable components that can be leveraged, such as:
    -   Page objects or screen objects.
    -   API clients or service layers.
    -   Test data generators.
    -   Fixtures or setup/teardown hooks.
-   **Identify Gaps:** Based on the scenario analysis, identify any missing components that will need to be created.

### 3. Create a Test Plan

Based on your analysis, create a concise and actionable test plan.

```markdown
# Test Plan: [Scenario Name]

## 1. Scenario Overview
-   A brief, 2-3 sentence description of the end-to-end workflow being tested.

## 2. Systems Involved
-   A list of all the systems that will be touched during the test.

## 3. Test Flow
-   A high-level, step-by-step description of the test flow, from initial setup to final validation.

## 4. Framework Analysis
-   **Existing Components:** A list of reusable components that will be used.
-   **Components to Create:** A list of new components (e.g., page objects, utility functions) that need to be built.

## 5. Implementation Strategy
-   **Component-First Approach:** Plan to first build and validate individual, reusable components (e.g., page objects for each system) before orchestrating them in the final E2E test.
-   **Data Management:** All test data should be generated dynamically to ensure tests are independent and repeatable. Avoid hardcoded values.

## 6. Task Breakdown (Optional)
-   **Task 1: Build Components for [System 1]:** Create and validate the necessary page objects and utilities for the first system.
-   **Task 2: Build Components for [System 2]:** Create and validate the components for the second system.
-   **Task 3: E2E Integration Test:** Assemble the components from the previous tasks into a single, comprehensive E2E test.
```

### 4. Present the Plan

-   Share the test plan with the team or user for feedback and approval before beginning implementation.

## Best Practices

-   **Focus on WHAT, Not HOW:** The plan should define what needs to be built, leaving the specific implementation details to the developer.
-   **Promote Reusability:** Design the plan to encourage the creation of reusable components that can be used in other tests.
-   **Dynamic Data is Key:** Emphasize that all tests must use dynamically generated, unique data to avoid conflicts and ensure reliability.
-   **Keep it Concise:** The goal is to create a clear and actionable plan, not a lengthy, overly detailed document.
