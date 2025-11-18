# API Automation Best Practices

## Objective
Define best practices for API test automation that should be followed across all projects, emphasizing treating APIs as contracts, maintaining test independence, and building resilient automation frameworks.

## Context
Apply when:
- Building API test automation frameworks
- Testing REST, GraphQL, or gRPC APIs
- Implementing CI/CD integration for API tests
- Designing test data management strategies

## API Contract Definition

- Define API contracts clearly before writing tests including endpoints, request/response schemas, status codes, error codes, rate limits, and authentication methods
- Document the contract as the foundation for all test scenarios
- Use OpenAPI/Swagger specifications when available to auto-generate test scaffolding
- Version API contracts alongside test suites to maintain compatibility

## Test Design Principles

- Keep tests atomic and independent - each test should execute successfully regardless of other tests
- Avoid test interdependencies unless explicitly testing workflows
- Design tests to be idempotent where possible to enable safe re-execution
- Separate test logic from test data using fixtures or external configuration files
- Store payloads, headers, tokens, and environment URLs in dedicated data files
- Use descriptive test names that clearly indicate what is being validated

## Validation Strategies

- Validate beyond status codes - a 200 response can still contain incorrect data
- Check response fields, data types, field lengths, business rules, timestamps, and headers
- Implement JSON Schema validation for response structure verification
- Add basic performance thresholds (response time validation)
- Validate error responses are well-formed and contain meaningful messages
- Verify pagination, sorting, and filtering logic when applicable

## Negative Testing

- Automate negative tests intentionally to ensure APIs fail gracefully
- Test 400-series validations (bad requests, unauthorized, forbidden, not found)
- Verify behavior with wrong HTTP methods
- Test missing or invalid authentication scenarios
- Validate bad payload handling (malformed JSON, missing required fields, invalid data types)
- Check rate limit enforcement
- Test boundary conditions (empty strings, null values, maximum lengths, special characters)

## Environment Management

- Use environment-based configuration for dev, QA, staging, and production-like environments
- Store environment-specific settings in configuration files or environment variables
- Make environment switching seamless without code changes
- Never hardcode environment URLs or credentials in test code
- Use a configuration management approach that supports easy environment switching

## Authentication and Security

- Keep secrets encrypted and never commit them to version control
- Rotate tokens and credentials regularly
- Implement token refresh strategies for long-running test suites
- Store sensitive data in secure vaults or encrypted configuration
- Use separate test accounts with appropriate permissions
- Implement proper session management in workflow tests

## Retry and Resilience

- Add retries only for transient failures (network jitter, rate limits, eventual consistency)
- Never retry logic errors or bad payload scenarios
- Implement exponential backoff for rate-limited endpoints
- Set appropriate timeout values based on expected response times
- Handle async operations with proper polling or webhook verification

## Workflow Testing

- Build end-to-end workflow tests (auth → create → read → update → delete) but keep them separate
- Label workflow tests distinctly and run them separately from unit API tests
- Limit the number of workflow tests to critical business paths
- Design workflows to be self-contained with proper setup and teardown
- Use workflow tests to validate system integration points

## Test Data Management

- Design tests with idempotency in mind
- Implement cleanup strategies for non-idempotent operations (POST, DELETE)
- Use soft delete or temporary data tables when possible
- Add teardown steps to remove test data after execution
- Avoid polluting test environments with "test12345" data fossils
- Use data factories or builders for consistent test data generation

## Diagnostic Capabilities

- Make test failures diagnostic-friendly with clear error messages
- Log raw request and response payloads on failure
- Include timestamps and correlation IDs in test output
- Attach relevant logs or screenshots when applicable
- Provide context about what was expected vs what was received
- Use structured logging for easier debugging

## API Versioning

- Version API tests alongside API versions
- Keep separate test folders or tags per API version
- Maintain backward compatibility tests when supporting multiple versions
- Clearly mark deprecated endpoint tests
- Plan migration strategies when API versions are sunset

## CI/CD Integration

- Trigger API tests on pull requests for fast feedback
- Run smoke tests on every commit
- Execute full regression suites nightly or on deployment
- Integrate tests into deployment pipelines as quality gates
- Ensure test execution is fast enough for CI/CD workflows
- Fail builds on critical test failures
- Generate and archive test reports for historical analysis

## Contract Testing

- Implement contract testing using tools like PACT, Dredd, or schema validators
- Catch breaking changes instantly before they reach production
- Maintain backward compatibility through contract verification
- Use contract tests to validate provider-consumer agreements
- Run contract tests as part of the deployment pipeline

## Test Suite Health Monitoring

- Track flake rates and investigate unstable tests
- Monitor slow tests and optimize performance
- Review skipped tests regularly and fix or remove them
- Measure endpoint coverage to identify gaps
- Maintain a healthy test suite that provides confidence
- Remove obsolete tests that no longer provide value
- Refactor tests when they become difficult to maintain

## Framework and Tooling

- Choose API testing frameworks that support the technology stack (REST, GraphQL, gRPC)
- Use assertion libraries with clear, readable syntax
- Implement reusable helper functions for common operations
- Create base classes or utilities for authentication, request building, and response validation
- Use data-driven testing approaches for testing multiple scenarios
- Leverage parallel execution capabilities for faster test runs

## Documentation and Reporting

- Document test scenarios and their purpose
- Generate clear test reports with pass/fail statistics
- Include test coverage metrics in reports
- Provide examples of how to run tests locally and in CI/CD
- Maintain a test strategy document outlining approach and scope
- Keep test documentation updated as APIs evolve

## References
- [REST API Testing Best Practices](https://restfulapi.net/)
- [API Testing Tools Comparison](https://www.postman.com/api-testing/)
- [Contract Testing with PACT](https://docs.pact.io/)

## Related Rules
- [API Design Principles](../backend/api-design-principles.md)
- [Testing Strategies](./testing-strategies.md)
- [Security Best Practices](../security-devops/security-best-practices.md)
