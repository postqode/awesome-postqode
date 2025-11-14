# PostQode Rules

A comprehensive collection of rules to guide PostQode's behavior across your development projects. Rules provide persistent context, coding standards, and best practices that PostQode follows automatically.

## 📋 Table of Contents

- [What are PostQode Rules?](#what-are-postqode-rules)
- [How Rules Work](#how-rules-work)
- [Rule Categories](#rule-categories)
- [Creating Your Own Rules](#creating-your-own-rules)
- [Rule Template](#rule-template)
- [Best Practices](#best-practices)

## What are PostQode Rules?

PostQode Rules are markdown files that provide system-level guidance to PostQode. They help you:

- 🎯 **Define Standards**: Establish coding conventions and best practices
- 🏗️ **Set Context**: Provide project-specific or framework-specific guidance
- 📚 **Share Knowledge**: Document team patterns and architectural decisions
- 🔧 **Configure Behavior**: Customize how PostQode approaches different tasks
- 🌍 **Scale Practices**: Apply consistent standards across projects

## How Rules Work

### Workspace Rules (Project-Specific)

Create rules for your current project:

```bash
/newrule
```

**Storage Location**: `.postqode/rules/` in your project directory

**Use Cases**:
- Project-specific coding standards
- Framework configurations for this project
- Team conventions for this codebase
- Architecture patterns for this application

### Global Rules (All Projects)

Create rules that apply everywhere:

```bash
/newglobalrule
```

**Storage Location**: `~/Documents/PostQode/Rules/`

**Use Cases**:
- Personal coding preferences
- Language-specific standards
- General best practices
- Cross-project conventions

### Rule Priority

When rules conflict, PostQode follows this priority:
1. **Workspace Rules** (highest priority)
2. **Global Rules**
3. **PostQode Defaults** (lowest priority)

## Rule Categories

### 🌐 Web Development

Modern web development standards and frameworks.

- **[React Best Practices](./web/react-best-practices.md)** - Component patterns, hooks, state management
- **[Vue.js Guidelines](./web/vue-guidelines.md)** - Composition API, reactivity, component structure
- **[Next.js Conventions](./web/nextjs-conventions.md)** - App router, server components, data fetching
- **[TypeScript Standards](./web/typescript-standards.md)** - Type safety, interfaces, generics
- **[CSS/Tailwind Patterns](./web/css-tailwind-patterns.md)** - Utility-first CSS, responsive design

### 🔧 Backend Development

Server-side development patterns and APIs.

- **[Node.js Best Practices](./backend/nodejs-best-practices.md)** - Express, async patterns, error handling
- **[Python Django Guidelines](./backend/python-django-guidelines.md)** - Models, views, DRF patterns
- **[API Design Principles](./backend/api-design-principles.md)** - REST, GraphQL, versioning
- **[Database Patterns](./backend/database-patterns.md)** - Schema design, migrations, queries

### 🧪 Testing & Quality

Testing strategies and code quality standards.

- **[Testing Strategies](./testing/testing-strategies.md)** - Unit, integration, E2E testing
- **[Code Review Guidelines](./testing/code-review-guidelines.md)** - Review checklist, feedback patterns
- **[Performance Optimization](./testing/performance-optimization.md)** - Profiling, caching, optimization

### 📱 Mobile Development

Mobile app development standards.

- **[React Native Standards](./mobile/react-native-standards.md)** - Navigation, state, native modules
- **[Flutter Guidelines](./mobile/flutter-guidelines.md)** - Widgets, state management, platform code
- **[iOS Swift Conventions](./mobile/ios-swift-conventions.md)** - SwiftUI, UIKit, architecture
- **[Android Kotlin Patterns](./mobile/android-kotlin-patterns.md)** - Jetpack Compose, coroutines, MVVM

### 🤖 AI & Machine Learning

ML and data science project standards.

- **[ML Project Structure](./ai-ml/ml-project-structure.md)** - Notebooks, experiments, models
- **[Data Science Workflows](./ai-ml/data-science-workflows.md)** - EDA, preprocessing, validation
- **[Model Development Guidelines](./ai-ml/model-development-guidelines.md)** - Training, evaluation, deployment

### 🔐 Security & DevOps

Security practices and deployment patterns.

- **[Security Best Practices](./security-devops/security-best-practices.md)** - Authentication, encryption, OWASP
- **[CI/CD Patterns](./security-devops/cicd-patterns.md)** - Pipeline design, testing, deployment
- **[Docker Guidelines](./security-devops/docker-guidelines.md)** - Dockerfile best practices, multi-stage builds

### 📝 Documentation

Documentation standards and templates.

- **[Documentation Standards](./documentation/documentation-standards.md)** - README, API docs, comments
- **[README Templates](./documentation/readme-templates.md)** - Project documentation structure
- **[API Documentation](./documentation/api-documentation.md)** - OpenAPI, endpoint documentation

## Creating Your Own Rules

### Rule Structure

A well-crafted rule should include:

1. **Title**: Clear, descriptive name
2. **Objective**: What the rule aims to achieve
3. **Context**: When and where to apply
4. **Guidelines**: Specific, actionable instructions
5. **Examples**: Code samples showing do's and don'ts
6. **References**: Links to official docs or resources

### Rule Template

```markdown
# Rule Name

## Objective
Brief description of what this rule accomplishes and why it matters.

## Context
When to apply this rule:
- Project types (e.g., React apps, Node.js APIs)
- Frameworks or libraries involved
- Specific scenarios or use cases

## Guidelines

### Core Principles
- Key principle 1 with explanation
- Key principle 2 with explanation
- Key principle 3 with explanation

### Do This ✅

**Pattern 1: Descriptive Name**
```language
// Good example with explanation
const example = "code here";
```
Why this works: Explanation of benefits.

**Pattern 2: Another Pattern**
```language
// Another good example
```

### Avoid This ❌

**Anti-pattern 1: What Not To Do**
```language
// Bad example
const badExample = "avoid this";
```
Why this is problematic: Explanation of issues.

## Detailed Examples

### Example 1: Common Scenario
```language
// Complete working example
// With comments explaining key points
```

### Example 2: Edge Case
```language
// How to handle special situations
```

## Best Practices

1. **Practice 1**: Detailed explanation
2. **Practice 2**: Detailed explanation
3. **Practice 3**: Detailed explanation

## Common Pitfalls

- **Pitfall 1**: What to watch out for and how to avoid
- **Pitfall 2**: Common mistake and solution
- **Pitfall 3**: Edge case to be aware of

## References
- [Official Documentation](https://example.com)
- [Related Guide](https://example.com)
- [Community Resources](https://example.com)

## Related Rules
- [Related Rule 1](./path/to/rule.md)
- [Related Rule 2](./path/to/rule.md)
```

## Best Practices

### Writing Effective Rules

**Be Specific**
- Provide concrete examples, not vague advice
- Include actual code snippets
- Show both good and bad patterns

**Be Actionable**
- Give clear instructions PostQode can follow
- Avoid ambiguous language
- Include decision criteria

**Be Contextual**
- Explain when rules apply
- Mention exceptions
- Provide reasoning

**Be Maintainable**
- Keep rules focused on one topic
- Update rules as standards evolve
- Remove outdated practices

### Organizing Rules

**Single Responsibility**
- One rule = one concept
- Split complex topics into multiple rules
- Link related rules together

**Clear Naming**
- Use descriptive, searchable names
- Follow consistent naming patterns
- Include framework/language in name

**Proper Categorization**
- Place rules in appropriate directories
- Use consistent category structure
- Cross-reference when needed

### Testing Rules

Before sharing a rule:

1. **Test with PostQode**: Verify PostQode follows the rule correctly
2. **Check Examples**: Ensure all code examples work
3. **Validate Links**: Confirm all references are accessible
4. **Review Clarity**: Have someone else read it
5. **Update README**: Add rule to category listing

## Contributing Rules

We welcome community contributions! To add a rule:

1. **Fork** the repository
2. **Create** your rule following the template
3. **Test** with PostQode
4. **Add** to appropriate category
5. **Update** this README
6. **Submit** pull request

### Contribution Checklist

- [ ] Rule follows the template structure
- [ ] Includes practical code examples
- [ ] Examples are tested and working
- [ ] All links are valid
- [ ] Markdown is properly formatted
- [ ] Added to category in README
- [ ] Tested with PostQode
- [ ] No sensitive information included

## Rule Maintenance

### Updating Rules

Rules should be updated when:
- Framework versions change significantly
- Best practices evolve
- Community feedback suggests improvements
- Errors or outdated info is found

### Deprecating Rules

When a rule becomes obsolete:
1. Add deprecation notice at the top
2. Explain why it's deprecated
3. Link to replacement rule if available
4. Keep for historical reference

## Examples of Good Rules

### Minimal Rule (Quick Reference)
```markdown
# Use Async/Await Over Promises

## Objective
Prefer async/await syntax for cleaner asynchronous code.

## Guidelines
✅ Use async/await for better readability
❌ Avoid promise chains when async/await works

## Example
```javascript
// Good
async function fetchData() {
  const response = await fetch(url);
  return await response.json();
}

// Avoid
function fetchData() {
  return fetch(url)
    .then(response => response.json());
}
```
```

### Comprehensive Rule (Detailed Guide)
See any of the category rules for examples of comprehensive documentation.

## Support

- 📖 [PostQode Documentation](https://docs.postqode.ai)
- 💬 [Community Discord](https://discord.gg/postqode)
- 🐛 [Report Issues](https://github.com/postqode/awesome-postqode/issues)

---

**[← Back to Main](../README.md)** | **[Explore Workflows →](../workflows/README.md)**
