## Brief overview

This rule defines best practices for unit testing with Jest. It emphasizes test isolation, proper mocking strategies, and comprehensive coverage for JavaScript and TypeScript applications.

## Test organization and structure

- Use Jest's recommended folder structure (__tests__, __mocks__, fixtures)
- Organize tests by feature or module structure
- Create test files with .test.js or .spec.js extensions
- Implement proper test setup and configuration files
- Use descriptive test names and clear documentation
- Separate unit tests from integration and E2E tests
- Create custom matchers and test utilities
- Implement proper test data factories and fixtures

## Test writing best practices

- Write tests using describe(), it(), and expect() patterns
- Use descriptive test names that explain the functionality
- Implement proper setup and teardown with beforeEach() and afterEach()
- Write atomic tests that focus on single units of functionality
- Use proper assertions with clear expected vs actual comparisons
- Implement proper error handling and edge case testing
- Use test.each() for data-driven testing with multiple scenarios
- Create meaningful test descriptions and documentation
- Use proper test grouping with describe() blocks

## Mocking and test doubles

- Use Jest's mocking capabilities for external dependencies
- Implement proper module mocking with jest.mock()
- Create mock implementations for APIs and services
- Use spy functions for monitoring function calls
- Implement proper mock data and responses
- Use factory functions for creating test objects
- Mock timers and asynchronous operations appropriately
- Implement proper mock cleanup and restoration
- Use dependency injection for testability

## Assertions and matchers

- Use Jest's built-in matchers (toBe, toEqual, toContain)
- Create custom matchers for domain-specific validations
- Implement proper async/await testing with resolves/rejects
- Use proper error message assertions and validation
- Test for null/undefined values appropriately
- Implement proper array and object property testing
- Use proper numeric and floating-point comparisons
- Create readable assertion messages with custom matchers

## Test configuration and setup

- Use proper Jest configuration files (jest.config.js)
- Implement appropriate test environments and variables
- Use setupFilesAfterEnv for global test setup
- Configure proper coverage collection and reporting
- Implement proper transform and preprocessing configurations
- Use appropriate test timeout and retry settings
- Configure proper test reporters and output formats

## Async testing patterns

- Test promises with proper resolve/reject handling
- Use async/await patterns for asynchronous code testing
- Implement proper timer mocking with jest.useFakeTimers()
- Test async functions with proper error handling
- Use proper callback and event-driven testing
- Implement proper race condition and concurrency testing
- Test async iterators and generators
- Use proper async/await in test hooks and setup

## Component and React testing

- Use React Testing Library for component testing
- Implement proper shallow rendering with shallow()
- Test component lifecycle methods and hooks
- Use proper props and state testing
- Implement proper event handling and callback testing
- Test component integration and user interactions
- Use proper snapshot testing for UI consistency
- Implement proper context and provider testing

## Coverage and quality

- Configure Jest coverage with appropriate thresholds
- Use proper coverage collection and reporting
- Implement coverage exclusions for non-critical code
- Monitor coverage trends and set quality gates
- Use proper branch coverage for pull requests
- Implement coverage badges and reporting in CI/CD
- Use proper coverage visualization and analysis tools

## Integration testing strategies

- Test module integration and dependencies
- Implement proper API integration testing
- Use proper database integration testing with test databases
- Test file system and external service integrations
- Implement proper end-to-end workflow testing
- Use proper environment configuration for integration tests
- Test error handling and recovery scenarios
- Implement proper performance and load testing

## Performance and optimization

- Use proper test performance monitoring
- Implement test parallelization for faster execution
- Use proper test caching and optimization strategies
- Monitor test execution times and identify slow tests
- Implement proper memory and resource management in tests
- Use proper test data optimization and cleanup
- Implement selective test execution for focused testing
- Use proper test profiling and analysis tools

## Debugging and troubleshooting

- Use Jest's debugging capabilities and breakpoints
- Implement proper console.log() and debugging output
- Use proper test filtering and focused execution
- Implement proper error message analysis and reporting
- Use proper test isolation for debugging specific issues
- Implement proper snapshot debugging and comparison
- Use proper test watch mode for development
- Implement proper source maps and error tracking

## CI/CD integration

- Use Jest's CI integration with proper configuration
- Implement proper test automation in build pipelines
- Use proper test reporting and artifact collection
- Configure proper test environments for different stages
- Implement proper test result notifications and integration
- Use proper test parallelization in CI environments
- Implement proper test caching and optimization for CI
- Configure proper test quality gates and coverage requirements

## Best practices summary

- Write tests first (TDD) when possible
- Keep tests simple and focused on single responsibilities
- Use descriptive test names and proper documentation
- Implement proper test isolation and independence
- Use appropriate mocking and test doubles
- Maintain high test coverage with meaningful tests
- Regularly review and refactor test code for maintainability
- Use proper test data management and cleanup strategies
- Implement proper error handling and edge case coverage
