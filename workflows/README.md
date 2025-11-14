# PostQode Workflows

Automated sequences and reusable patterns for common development tasks. Workflows help you streamline repetitive processes and maintain consistency across your projects.

## 📋 Table of Contents

- [What are PostQode Workflows?](#what-are-postqode-workflows)
- [How Workflows Work](#how-workflows-work)
- [Workflow Categories](#workflow-categories)
- [Creating Your Own Workflows](#creating-your-own-workflows)
- [Workflow Template](#workflow-template)
- [Best Practices](#best-practices)

## What are PostQode Workflows?

PostQode Workflows are automated sequences that guide PostQode through multi-step processes. They help you:

- ⚡ **Automate Tasks**: Execute complex sequences automatically
- 🔄 **Ensure Consistency**: Follow the same steps every time
- 📦 **Reuse Patterns**: Apply proven solutions across projects
- 🎯 **Save Time**: Reduce manual, repetitive work
- 📚 **Share Knowledge**: Document and share team processes

## How Workflows Work

### Workspace Workflows (Project-Specific)

Create workflows for your current project:

```bash
/newworkflow
```

**Storage Location**: `.postqode/workflows/` in your project directory

**Use Cases**:
- Project-specific automation
- Custom build processes
- Team-specific procedures
- Application-specific tasks

### Global Workflows (All Projects)

Create workflows that apply everywhere:

```bash
/newglobalworkflow
```

**Storage Location**: `~/Documents/PostQode/Workflows/`

**Use Cases**:
- Personal automation preferences
- Language-agnostic processes
- Cross-project patterns
- Reusable templates

### Workflow Execution

Workflows can be:
- **Triggered manually** via commands
- **Invoked by name** in chat
- **Chained together** for complex automation
- **Parameterized** for flexibility

## Workflow Categories

### 🏗️ Project Setup
- **[New React Project](./examples/new-react-project.md)** - Initialize React app with best practices
- **[API Project Setup](./examples/api-project-setup.md)** - Set up Node.js/Express API
- **[Full-Stack Starter](./examples/fullstack-starter.md)** - Complete full-stack project scaffold

### 🧩 Component Generation
- **[React Component](./examples/component-generator.md)** - Generate React component with tests
- **[Vue Component](./examples/vue-component-generator.md)** - Create Vue component with composition API
- **[API Endpoint](./examples/api-endpoint-setup.md)** - Generate REST endpoint with validation

### 🧪 Testing Workflows
- **[Test Suite Creator](./examples/test-suite-creator.md)** - Generate comprehensive test suite
- **[E2E Test Setup](./examples/e2e-test-setup.md)** - Set up end-to-end testing
- **[Test Coverage Report](./examples/test-coverage-report.md)** - Generate and analyze coverage

### 🚀 Deployment
- **[Docker Deploy](./examples/docker-deploy.md)** - Containerize and deploy application
- **[CI/CD Setup](./examples/cicd-setup.md)** - Configure GitHub Actions/GitLab CI
- **[Production Checklist](./examples/production-checklist.md)** - Pre-deployment verification

### 🔧 Refactoring
- **[Component Refactor](./examples/component-refactor.md)** - Modernize component patterns
- **[API Versioning](./examples/api-versioning.md)** - Add API version support
- **[Database Migration](./examples/database-migration.md)** - Create and apply migrations

### 📝 Documentation
- **[API Docs Generator](./examples/api-docs-generator.md)** - Generate OpenAPI documentation
- **[README Creator](./examples/readme-creator.md)** - Create comprehensive README
- **[Changelog Update](./examples/changelog-update.md)** - Maintain CHANGELOG.md

## Creating Your Own Workflows

### Workflow Structure

A well-designed workflow should include:

1. **Name**: Clear, action-oriented title
2. **Purpose**: What the workflow accomplishes
3. **Prerequisites**: Required tools, dependencies, or setup
4. **Steps**: Ordered sequence of actions
5. **Parameters**: Configurable inputs
6. **Validation**: Checks to ensure success
7. **Outputs**: What gets created or modified

### Workflow Template

```markdown
# Workflow Name

## Purpose
Brief description of what this workflow accomplishes and when to use it.

## Prerequisites
- Required tool or dependency 1
- Required tool or dependency 2
- Required setup or configuration

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| param1 | string | Yes | - | Description of parameter |
| param2 | boolean | No | true | Description of parameter |
| param3 | array | No | [] | Description of parameter |

## Steps

### Step 1: Descriptive Step Name
**Action**: What PostQode should do
**Details**: Additional context or instructions
**Validation**: How to verify this step succeeded

```language
// Example code or command
```

### Step 2: Next Step Name
**Action**: What PostQode should do
**Details**: Additional context or instructions
**Validation**: How to verify this step succeeded

```language
// Example code or command
```

### Step 3: Continue Pattern...

## Outputs

### Created Files
- `path/to/file1.ext` - Description of file
- `path/to/file2.ext` - Description of file

### Modified Files
- `path/to/existing.ext` - What was changed

### Generated Artifacts
- Description of other outputs (logs, reports, etc.)

## Validation Checklist

- [ ] Validation item 1
- [ ] Validation item 2
- [ ] Validation item 3

## Example Usage

### Basic Usage
\`\`\`bash
# How to invoke this workflow
/workflow workflow-name param1="value1"
\`\`\`

### Advanced Usage
\`\`\`bash
# More complex example
/workflow workflow-name param1="value1" param2=false param3=["item1","item2"]
\`\`\`

## Common Issues

### Issue 1: Problem Description
**Symptom**: What the user might see
**Cause**: Why this happens
**Solution**: How to fix it

### Issue 2: Another Problem
**Symptom**: What the user might see
**Cause**: Why this happens
**Solution**: How to fix it

## Related Workflows
- [Related Workflow 1](./related-workflow-1.md)
- [Related Workflow 2](./related-workflow-2.md)

## Related Rules
- [Related Rule 1](../rules/category/rule-name.md)
- [Related Rule 2](../rules/category/rule-name.md)
```

## Best Practices

### Designing Effective Workflows

**Be Atomic**
- Each step should be a single, clear action
- Steps should be independently verifiable
- Avoid combining unrelated operations

**Be Idempotent**
- Workflow should be safely re-runnable
- Check for existing files/resources before creating
- Handle partial completion gracefully

**Be Flexible**
- Use parameters for customization
- Provide sensible defaults
- Support different project structures

**Be Validated**
- Include verification steps
- Check prerequisites before starting
- Validate outputs after completion

### Workflow Organization

**Clear Naming**
- Use action verbs (Create, Setup, Generate, Deploy)
- Be specific about what's automated
- Include technology/framework in name

**Logical Grouping**
- Group related workflows together
- Use consistent category structure
- Cross-reference related workflows

**Version Awareness**
- Note framework/tool versions
- Update for breaking changes
- Maintain backward compatibility when possible

### Error Handling

**Anticipate Failures**
- Check prerequisites upfront
- Validate inputs before processing
- Provide clear error messages

**Graceful Degradation**
- Allow partial completion
- Provide rollback instructions
- Save progress when possible

**User Guidance**
- Explain what went wrong
- Suggest corrective actions
- Link to relevant documentation

## Example Workflows

### Simple Workflow (Quick Task)

```markdown
# Create React Component

## Purpose
Generate a new React functional component with TypeScript and basic styling.

## Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| name | string | Yes | - | Component name (PascalCase) |
| path | string | No | src/components | Directory path |

## Steps

### Step 1: Create Component File
Create `{path}/{name}.tsx` with functional component structure.

### Step 2: Create Styles File
Create `{path}/{name}.module.css` with basic styles.

### Step 3: Create Test File
Create `{path}/{name}.test.tsx` with basic test suite.

### Step 4: Update Index
Add export to `{path}/index.ts`.

## Outputs
- Component file with TypeScript
- CSS module for styling
- Test file with basic tests
- Updated barrel export
```

### Complex Workflow (Multi-Step Process)

See the [examples](./examples/) directory for comprehensive workflow examples.

## Workflow Patterns

### Sequential Pattern
Steps execute one after another, each depending on the previous.

```
Step 1 → Step 2 → Step 3 → Complete
```

### Conditional Pattern
Steps execute based on conditions or parameters.

```
Step 1 → Check Condition
         ├─ If True → Step 2A → Complete
         └─ If False → Step 2B → Complete
```

### Parallel Pattern
Independent steps can execute simultaneously.

```
Step 1 → ┬─ Step 2A ─┬→ Step 4 → Complete
         └─ Step 2B ─┘
```

### Loop Pattern
Repeat steps for multiple items or until condition met.

```
Step 1 → For Each Item → Step 2 → Step 3 → Next Item → Complete
```

## Testing Workflows

Before sharing a workflow:

1. **Test Execution**: Run the complete workflow
2. **Test Parameters**: Try different parameter combinations
3. **Test Edge Cases**: Handle unusual inputs
4. **Test Failures**: Verify error handling
5. **Test Cleanup**: Ensure proper cleanup on failure

## Contributing Workflows

We welcome community contributions! To add a workflow:

1. **Fork** the repository
2. **Create** your workflow following the template
3. **Test** thoroughly with PostQode
4. **Document** all parameters and steps
5. **Add** to appropriate category
6. **Update** this README
7. **Submit** pull request

### Contribution Checklist

- [ ] Workflow follows the template structure
- [ ] All steps are clearly documented
- [ ] Parameters are well-defined
- [ ] Includes validation steps
- [ ] Tested with PostQode
- [ ] Error handling is robust
- [ ] Examples are provided
- [ ] Added to category in README
- [ ] No sensitive information included

## Workflow Maintenance

### Updating Workflows

Update workflows when:
- Tool versions change
- Better patterns emerge
- Community feedback suggests improvements
- Bugs or issues are discovered

### Deprecating Workflows

When a workflow becomes obsolete:
1. Add deprecation notice at the top
2. Explain why it's deprecated
3. Link to replacement workflow
4. Keep for historical reference

## Advanced Features

### Workflow Chaining
Combine multiple workflows for complex automation:

```bash
/workflow setup-project && /workflow add-component name="Header"
```

### Parameterized Workflows
Pass dynamic values to customize behavior:

```bash
/workflow create-api endpoint="users" methods=["GET","POST"]
```

### Conditional Execution
Execute workflows based on project state:

```bash
/workflow deploy-app environment="production" if-tests-pass=true
```

## Support

- 📖 [PostQode Documentation](https://docs.postqode.ai)
- 💬 [Community Discord](https://discord.gg/postqode)
- 🐛 [Report Issues](https://github.com/postqode/awesome-postqode/issues)

---

**[← Back to Main](../README.md)** | **[Explore Rules →](../rules/README.md)**
