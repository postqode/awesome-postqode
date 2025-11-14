## Brief overview

This rule defines best practices for building Python applications that integrate Large Language Models (LLMs) and machine learning workflows. It emphasizes proper prompt engineering, response handling, and integration patterns for production-ready LLM-powered applications.

## LLM integration patterns

- Use structured prompts with clear system messages and user message separation
- Implement proper error handling for LLM API failures and rate limits
- Design fallback mechanisms when LLM responses are unreliable or unavailable
- Use response validation to ensure LLM outputs match expected schemas
- Implement caching for expensive LLM calls to reduce costs and improve latency
- Use streaming responses for long-form content generation
- Design idempotent operations that can be safely retried

## Prompt engineering best practices

- Write clear, specific prompts with explicit instructions and constraints
- Use few-shot examples to guide LLM responses toward desired format
- Implement prompt templates with variable substitution for consistency
- Include output format specifications (JSON, markdown, code blocks)
- Use chain-of-thought prompting for complex reasoning tasks
- Implement prompt versioning and A/B testing for optimization
- Store prompts separately from code for easy modification and testing

## Error handling and resilience

- Implement exponential backoff for rate-limited LLM APIs
- Use circuit breakers to prevent cascading failures
- Log LLM requests and responses for debugging and audit trails
- Implement graceful degradation when LLM services are unavailable
- Use timeout mechanisms to prevent hanging on LLM responses
- Validate LLM responses against schemas before processing
- Implement retry logic with different prompts for failed generations

## Performance optimization

- Batch multiple small requests into single LLM calls when possible
- Use smaller, specialized models for simple tasks to reduce costs
- Implement response caching with appropriate TTL based on content volatility
- Use async/await patterns for concurrent LLM operations
- Monitor token usage and implement cost tracking
- Use model routing based on task complexity and requirements
- Implement request queuing for high-volume scenarios

## Security and privacy

- Never log or store sensitive user data in LLM prompts
- Implement data sanitization before sending to LLMs
- Use environment-specific API keys and configuration
- Implement audit logging for LLM access and usage patterns
- Filter or redact PII from LLM responses when necessary
- Use role-based access control for LLM-powered features
- Implement data retention policies for LLM interactions

## Testing strategies

- Create mock LLM responses for unit testing business logic
- Implement integration tests with actual LLM APIs in staging
- Test edge cases: empty responses, malformed JSON, rate limits
- Use deterministic seeds for reproducible LLM behavior in tests
- Test prompt variations to ensure robustness
- Implement performance tests for LLM response times
- Test fallback mechanisms and error handling paths

## Code organization

- Separate LLM client code from business logic
- Create dedicated modules for prompt templates and management
- Implement factory patterns for different LLM providers (OpenAI, Anthropic, etc.)
- Use configuration files for model parameters and API endpoints
- Create abstractions for switching between LLM providers
- Implement response processors for different output formats
- Separate cost tracking and monitoring components

## Monitoring and observability

- Track LLM response times, success rates, and error patterns
- Monitor token usage and costs per feature or user
- Implement alerting for unusual LLM behavior or performance degradation
- Use structured logging for LLM requests and responses
- Implement dashboards for LLM usage analytics
- Track prompt effectiveness and response quality metrics
- Monitor API rate limits and implement throttling

## Integration patterns

- Use message queues for async LLM processing workflows
- Implement webhook patterns for long-running LLM tasks
- Design event-driven architectures for LLM-powered features
- Use background jobs for batch LLM processing
- Implement real-time updates for streaming LLM responses
- Design microservices around specific LLM capabilities
- Use API gateways for LLM service management

## Configuration management

- Use environment variables for LLM API keys and endpoints
- Implement feature flags for LLM-powered functionality
- Create configuration schemas for different LLM models and providers
- Use separate configurations for development, staging, and production
- Implement runtime configuration updates without service restarts
- Store prompt templates in external files for easy updates
- Use configuration validation for LLM parameters and limits
