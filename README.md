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
│   │   ├── frameworks/
│   │   │   ├── cypress-e2e-testing.md
│   │   │   ├── jest-unit-testing.md
│   │   │   └── playwright-e2e-testing.md
│   │   ├── principles/
│   │   │   ├── context-driven-testing.md
│   │   │   ├── test-automation-design-patterns.md
│   │   │   ├── test-automation-framework-guidelines.md
│   │   │   └── testing-strategies.md
│   │   └── types/
│   │       └── api-automation-best-practices.md
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
    ├── development/         # Development workflows
    │   └── fix-bug.md
    ├── examples/            # Example workflows
    │   └── component-generator.md
    ├── project-management/  # Project management workflows
    │   └── gather-feature-context.md
    └── testing/             # Testing workflows
        ├── create-automation-tests.md
        ├── create-test-charters.md
        ├── heal-failing-tests.md
        ├── plan-e2e-tests.md
        └── review-test-suite.md
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
