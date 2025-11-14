# Awesome PostQode

A curated collection of **rules** and **workflows** for [PostQode](https://postqode.ai) - your AI-powered coding assistant. Enhance your development experience with persistent guidance, best practices, and automated workflows.

## 📚 What's Inside

### 🎯 [Rules](./rules/)
Persistent instructions that guide PostQode's behavior across your projects. Define coding standards, establish conventions, and share team knowledge.

**[Explore Rules →](./rules/README.md)**

### ⚡ [Workflows](./workflows/)
Automated sequences and reusable patterns for common development tasks. Streamline your workflow with pre-built automation.

**[Explore Workflows →](./workflows/README.md)**

## 🚀 Quick Start

### Using Rules

**Workspace Rules** (Project-Specific)
```bash
# In PostQode chat
/newrule
```
Stored in `.postqode/rules/` within your project.

**Global Rules** (All Projects)
```bash
# In PostQode chat
/newglobalrule
```
Stored in `~/Documents/PostQode/Rules/`.

### Using Workflows

**Workspace Workflows** (Project-Specific)
```bash
# In PostQode chat
/newworkflow
```
Stored in `.postqode/workflows/` within your project.

**Global Workflows** (All Projects)
```bash
# In PostQode chat
/newglobalworkflow
```
Stored in `~/Documents/PostQode/Workflows/`.

## 📖 Documentation

- **[Rules Documentation](./rules/README.md)** - Learn about creating and using rules
- **[Workflows Documentation](./workflows/README.md)** - Learn about creating and using workflows
- **[PostQode Docs](https://docs.postqode.ai)** - Official PostQode documentation

## 🌟 Featured Content

### Web Development
- **[React Best Practices](./rules/web/react-best-practices.md)** - Modern React development with hooks, TypeScript, and performance optimization
- **[TypeScript Standards](./rules/web/typescript-standards.md)** - Type safety, interfaces, generics, and utility types
- **[Vue.js Best Practices](./rules/web/vuejs-best-practices.md)** - Modern Vue 3 with Composition API, reactivity patterns, and component architecture
- **[Angular Best Practices](./rules/web/angular-best-practices.md)** - Modern Angular with TypeScript, RxJS, and dependency injection
- **[Svelte Best Practices](./rules/web/svelte-best-practices.md)** - Reactive programming with Svelte 5 and component composition

### Backend Development
- **[API Design Principles](./rules/backend/api-design-principles.md)** - RESTful API design, HTTP methods, and versioning
- **[Python Django Best Practices](./rules/backend/python-django-best-practices.md)** - Django web development with proper project structure, ORM usage, and security practices

### Testing
- **[Testing Strategies](./rules/testing/testing-strategies.md)** - Test pyramid, unit/integration/E2E testing approaches
- **[API Automation Best Practices](./rules/testing/api-automation-best-practices.md)** - Comprehensive API testing guidelines
- **[Jest Unit Testing](./rules/testing/jest-unit-testing.md)** - JavaScript/TypeScript unit testing with mocking and coverage
- **[Cypress E2E Testing](./rules/testing/cypress-e2e-testing.md)** - End-to-end testing with Cypress automation
- **[Playwright E2E Testing](./rules/testing/playwright-e2e-testing.md)** - Modern browser automation with multi-browser support
- **[Test Automation Design Patterns](./rules/testing/test-automation-design-patterns.md)** - POM, data-driven testing, and locator strategies

### Mobile Development
- **[React Native Best Practices](./rules/mobile/react-native-best-practices.md)** - Cross-platform mobile development patterns
- **[iOS Testing Best Practices](./rules/mobile/ios-testing-best-practices.md)** - XCTest and XCUITest guidelines
- **[Android Testing Best Practices](./rules/mobile/android-testing-best-practices.md)** - JUnit and Espresso testing patterns

### AI & Machine Learning
- **[Python LLM Workflow](./rules/ai-ml/python-llm-workflow.md)** - LLM integration patterns, prompt engineering, and response handling

### Security & DevOps
- **[Security Best Practices](./rules/security-devops/security-best-practices.md)** - OWASP Top 10, authentication, and security patterns
- **[Docker Best Practices](./rules/devops/docker-best-practices.md)** - Containerization, security practices, and container management

### Database
- **[SQL Best Practices](./rules/database/sql-best-practices.md)** - Database design, query optimization, and data management

### Languages
- **[JavaScript Best Practices](./rules/languages/javascript-best-practices.md)** - Modern JavaScript development with ES6+ features, async programming, and module organization

### Documentation
- **[Documentation Standards](./rules/documentation/documentation-standards.md)** - README structure, code comments, API documentation

### Popular Workflows
- **[Component Generator](./workflows/examples/component-generator.md)** - React component creation with TypeScript, tests, and styles

## 🤝 Contributing

We welcome contributions! Here's how you can help:

1. **Fork** this repository
2. **Create** a new branch for your contribution
3. **Add** your rule or workflow following our templates
4. **Submit** a pull request

### Contribution Guidelines

- Follow the provided templates for rules and workflows
- Include practical, actionable examples
- Keep content focused and specific
- Test with PostQode before submitting
- Ensure proper markdown formatting
- Update the appropriate README.md

## 📦 Repository Structure

```
awesome-postqode/
├── README.md                 # Main documentation (you are here)
├── LICENSE                   # MIT License
├── .gitignore               # Standard ignore patterns
├── rules/                    # PostQode Rules (24 comprehensive guides)
│   ├── README.md            # Rules documentation
│   ├── web/                 # Web development rules
│   │   ├── react-best-practices.md
│   │   ├── typescript-standards.md
│   │   ├── vuejs-best-practices.md
│   │   ├── angular-best-practices.md
│   │   └── svelte-best-practices.md
│   ├── backend/             # Backend development rules
│   │   ├── api-design-principles.md
│   │   └── python-django-best-practices.md
│   ├── testing/             # Testing & quality rules
│   │   ├── testing-strategies.md
│   │   ├── api-automation-best-practices.md
│   │   ├── jest-unit-testing.md
│   │   ├── cypress-e2e-testing.md
│   │   ├── playwright-e2e-testing.md
│   │   └── test-automation-design-patterns.md
│   ├── mobile/              # Mobile development rules
│   │   ├── react-native-best-practices.md
│   │   ├── ios-testing-best-practices.md
│   │   └── android-testing-best-practices.md
│   ├── ai-ml/               # AI & ML rules
│   │   └── python-llm-workflow.md
│   ├── security-devops/     # Security & DevOps rules
│   │   ├── security-best-practices.md
│   │   └── docker-best-practices.md
│   ├── database/             # Database rules
│   │   └── sql-best-practices.md
│   ├── languages/            # Language-specific rules
│   │   └── javascript-best-practices.md
│   └── documentation/       # Documentation rules
│       └── documentation-standards.md
└── workflows/               # PostQode Workflows
    ├── README.md            # Workflows documentation
    └── examples/            # Example workflows
        └── component-generator.md
```

## 💡 Use Cases

### For Individual Developers
- Maintain consistent coding style across projects
- Automate repetitive tasks
- Learn best practices from the community
- Speed up development with proven patterns

### For Teams
- Enforce team coding standards
- Share knowledge and conventions
- Onboard new team members faster
- Standardize project structures

### For Organizations
- Maintain enterprise coding standards
- Ensure security and compliance
- Scale development practices
- Reduce code review time

## 🔗 Resources

- 📖 [PostQode Documentation](https://docs.postqode.ai)
- 💬 [Community Discord](https://discord.gg/postqode)
- 🐛 [Report Issues](https://github.com/postqode/awesome-postqode/issues)
- 🌐 [PostQode Website](https://postqode.ai)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

Inspired by the community's need for consistent, high-quality AI-assisted development practices.

---

**⭐ Star this repo** if you find it helpful! Share your custom rules and workflows with `#postqode` on social media.
