# React Component Generator

## Purpose
Automatically generate a complete React component with TypeScript, styles, tests, and documentation following best practices.

## Prerequisites
- React project with TypeScript configured
- Testing framework installed (Jest/Vitest + React Testing Library)
- CSS Modules or styled-components setup

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| name | string | Yes | - | Component name in PascalCase (e.g., "UserCard") |
| path | string | No | src/components | Directory path relative to project root |
| type | string | No | functional | Component type: "functional" or "page" |
| styling | string | No | css-modules | Styling approach: "css-modules", "styled-components", or "tailwind" |
| withTests | boolean | No | true | Generate test file |
| withStorybook | boolean | No | false | Generate Storybook story |

## Steps

### Step 1: Validate Component Name
**Action**: Verify the component name follows PascalCase convention
**Details**: 
- Check if name starts with uppercase letter
- Ensure no special characters except letters and numbers
- Warn if name doesn't follow React naming conventions

**Validation**: Component name is valid PascalCase

### Step 2: Create Component Directory
**Action**: Create directory structure for the component
**Details**:
```bash
{path}/{name}/
├── {name}.tsx
├── {name}.module.css (or styled.ts)
├── {name}.test.tsx
├── {name}.stories.tsx (if withStorybook)
└── index.ts
```

**Validation**: Directory created successfully

### Step 3: Generate Component File
**Action**: Create the main component file with TypeScript

**Details**: Generate functional component with:
- TypeScript interface for props
- Proper typing with React.FC or explicit return type
- JSDoc comments for documentation
- Accessibility attributes where applicable

```typescript
import React from 'react';
import styles from './{name}.module.css';

interface {name}Props {
  /**
   * Add prop descriptions here
   */
  className?: string;
}

/**
 * {name} component description
 * 
 * @example
 * ```tsx
 * <{name} />
 * ```
 */
export const {name}: React.FC<{name}Props> = ({ className }) => {
  return (
    <div className={`${styles.container} ${className || ''}`}>
      <h2>{name} Component</h2>
      <p>Component content goes here</p>
    </div>
  );
};
```

**Validation**: Component file created with proper TypeScript types

### Step 4: Generate Styles File
**Action**: Create styling file based on selected approach

**For CSS Modules**:
```css
.container {
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
}

.container h2 {
  margin: 0 0 0.5rem 0;
  font-size: 1.5rem;
  color: #333;
}

.container p {
  margin: 0;
  color: #666;
}
```

**For Styled Components**:
```typescript
import styled from 'styled-components';

export const Container = styled.div`
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;

  h2 {
    margin: 0 0 0.5rem 0;
    font-size: 1.5rem;
    color: #333;
  }

  p {
    margin: 0;
    color: #666;
  }
`;
```

**Validation**: Styles file created with base styling

### Step 5: Generate Test File
**Action**: Create comprehensive test file (if withTests is true)

**Details**:
```typescript
import { render, screen } from '@testing-library/react';
import { {name} } from './{name}';

describe('{name}', () => {
  it('renders without crashing', () => {
    render(<{name} />);
    expect(screen.getByText('{name} Component')).toBeInTheDocument();
  });

  it('applies custom className', () => {
    const { container } = render(<{name} className="custom-class" />);
    expect(container.firstChild).toHaveClass('custom-class');
  });

  // Add more tests as needed
});
```

**Validation**: Test file created with basic test cases

### Step 6: Generate Storybook Story
**Action**: Create Storybook story file (if withStorybook is true)

**Details**:
```typescript
import type { Meta, StoryObj } from '@storybook/react';
import { {name} } from './{name}';

const meta: Meta<typeof {name}> = {
  title: 'Components/{name}',
  component: {name},
  tags: ['autodocs'],
  argTypes: {
    // Define controls for props
  },
};

export default meta;
type Story = StoryObj<typeof {name}>;

export const Default: Story = {
  args: {
    // Default props
  },
};

export const CustomExample: Story = {
  args: {
    // Custom props example
  },
};
```

**Validation**: Storybook story created with examples

### Step 7: Create Barrel Export
**Action**: Create index.ts for clean imports

**Details**:
```typescript
export { {name} } from './{name}';
export type { {name}Props } from './{name}';
```

**Validation**: Barrel export file created

### Step 8: Update Parent Index
**Action**: Add export to parent directory's index.ts (if exists)

**Details**: Append to `{path}/index.ts`:
```typescript
export * from './{name}';
```

**Validation**: Parent index updated or created

## Outputs

### Created Files
- `{path}/{name}/{name}.tsx` - Main component file
- `{path}/{name}/{name}.module.css` - Component styles
- `{path}/{name}/{name}.test.tsx` - Test file (if withTests)
- `{path}/{name}/{name}.stories.tsx` - Storybook story (if withStorybook)
- `{path}/{name}/index.ts` - Barrel export

### Modified Files
- `{path}/index.ts` - Updated with new component export

## Validation Checklist

- [ ] Component name follows PascalCase convention
- [ ] All files created in correct directory
- [ ] TypeScript types are properly defined
- [ ] Component renders without errors
- [ ] Tests pass successfully
- [ ] Styles are applied correctly
- [ ] Component is exported from parent index
- [ ] No TypeScript errors in generated files

## Example Usage

### Basic Usage
```bash
# Generate a simple component
/workflow component-generator name="UserCard"
```

### Advanced Usage
```bash
# Generate component with all options
/workflow component-generator name="ProductCard" path="src/features/products/components" styling="styled-components" withStorybook=true
```

### Page Component
```bash
# Generate a page component
/workflow component-generator name="Dashboard" path="src/pages" type="page"
```

## Common Issues

### Issue 1: Component Already Exists
**Symptom**: Error message "Component already exists at path"
**Cause**: A component with the same name already exists in the target directory
**Solution**: 
- Choose a different name
- Specify a different path
- Delete the existing component if it's no longer needed

### Issue 2: Invalid Component Name
**Symptom**: Error message "Invalid component name"
**Cause**: Component name doesn't follow PascalCase or contains invalid characters
**Solution**: 
- Ensure name starts with uppercase letter
- Use only letters and numbers
- Follow PascalCase convention (e.g., "UserCard", not "userCard" or "user-card")

### Issue 3: Missing Dependencies
**Symptom**: Import errors or missing type definitions
**Cause**: Required packages not installed
**Solution**:
```bash
# Install required dependencies
npm install --save-dev @testing-library/react @testing-library/jest-dom
npm install --save-dev @storybook/react (if using Storybook)
```

### Issue 4: Path Not Found
**Symptom**: Error creating files in specified path
**Cause**: Target directory doesn't exist
**Solution**: The workflow will create the directory automatically, but ensure the path is valid relative to project root

## Related Workflows
- [Test Suite Creator](./test-suite-creator.md) - Generate additional tests
- [Storybook Setup](./storybook-setup.md) - Configure Storybook for project
- [Component Refactor](./component-refactor.md) - Modernize existing components

## Related Rules
- [React Best Practices](../../rules/web/react-best-practices.md)
- [TypeScript Standards](../../rules/web/typescript-standards.md)
- [Testing Strategies](../../rules/testing/testing-strategies.md)

## Notes

- This workflow follows React and TypeScript best practices
- Generated components use functional components with hooks
- All files include proper TypeScript typing
- Tests follow React Testing Library conventions
- Storybook stories use CSF 3.0 format
- Components are accessible by default with semantic HTML
