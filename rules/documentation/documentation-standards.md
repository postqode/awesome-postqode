# Documentation Standards

## Objective
Establish clear documentation practices for maintainable, accessible project documentation.

## Context
Apply when:
- Creating project README files
- Writing API documentation
- Documenting code with comments
- Creating user guides and tutorials

## Guidelines

### Core Principles

1. **Write for Humans**: Clear, concise, accessible language
2. **Keep it Updated**: Documentation should match current code
3. **Show, Don't Just Tell**: Include examples and code samples
4. **Structure Logically**: Organize information hierarchically
5. **Make it Searchable**: Use clear headings and keywords

### Do This ✅

**Pattern 1: README Structure**
```markdown
# Project Name

Brief description of what the project does (1-2 sentences).

## Features

- Feature 1
- Feature 2
- Feature 3

## Installation

\`\`\`bash
npm install project-name
\`\`\`

## Quick Start

\`\`\`typescript
import { Something } from 'project-name';

const example = new Something();
example.doThing();
\`\`\`

## Usage

### Basic Example

\`\`\`typescript
// Code example with explanation
\`\`\`

### Advanced Example

\`\`\`typescript
// More complex example
\`\`\`

## API Reference

### `functionName(param1, param2)`

Description of what the function does.

**Parameters:**
- `param1` (string): Description
- `param2` (number, optional): Description

**Returns:** Description of return value

**Example:**
\`\`\`typescript
const result = functionName('value', 42);
\`\`\`

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md)

## License

MIT © [Your Name]
```

**Pattern 2: Code Comments**
```typescript
/**
 * Calculates the total price including tax.
 * 
 * @param items - Array of items with price and quantity
 * @param taxRate - Tax rate as decimal (e.g., 0.1 for 10%)
 * @returns Total price including tax
 * 
 * @example
 * ```typescript
 * const items = [{ price: 10, quantity: 2 }];
 * const total = calculateTotal(items, 0.1);
 * // Returns: 22 (20 * 1.1)
 * ```
 */
function calculateTotal(
  items: Array<{ price: number; quantity: number }>,
  taxRate: number
): number {
  const subtotal = items.reduce(
    (sum, item) => sum + item.price * item.quantity,
    0
  );
  return subtotal * (1 + taxRate);
}

// Inline comments for complex logic
function processData(data: unknown) {
  // Validate input before processing
  if (!isValidData(data)) {
    throw new Error('Invalid data format');
  }

  // Transform data to internal format
  const normalized = normalizeData(data);

  // Apply business rules
  return applyRules(normalized);
}
```

**Pattern 3: API Documentation**
```markdown
## API Endpoints

### GET /api/users

Retrieve a list of users.

**Query Parameters:**
- `page` (number, optional): Page number (default: 1)
- `limit` (number, optional): Items per page (default: 20)
- `sort` (string, optional): Sort field and order (e.g., 'name:asc')

**Response:**
\`\`\`json
{
  "success": true,
  "data": [
    {
      "id": "123",
      "name": "John Doe",
      "email": "john@example.com"
    }
  ],
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 100
  }
}
\`\`\`

**Error Responses:**
- `400 Bad Request`: Invalid parameters
- `401 Unauthorized`: Missing or invalid authentication
- `500 Internal Server Error`: Server error

**Example:**
\`\`\`bash
curl -X GET "https://api.example.com/api/users?page=1&limit=10" \
  -H "Authorization: Bearer YOUR_TOKEN"
\`\`\`
```

### Avoid This ❌

**Anti-pattern 1: Vague Documentation**
```markdown
❌ Avoid
## Installation
Install the package.

## Usage
Use the functions.

✅ Better
## Installation
\`\`\`bash
npm install package-name
\`\`\`

## Usage
\`\`\`typescript
import { createUser } from 'package-name';

const user = await createUser({
  name: 'John Doe',
  email: 'john@example.com'
});
\`\`\`
```

**Anti-pattern 2: Outdated Documentation**
```typescript
// ❌ Outdated comment
/**
 * Gets user by ID from database
 * @deprecated Use getUserById instead
 */
function getUser(id: string) {
  // Function was renamed but comment not updated
}

// ✅ Keep comments current
/**
 * Retrieves user by ID from cache or database
 */
function getUserById(id: string) {
  // Implementation
}
```

## Best Practices

### 1. README Essentials
```markdown
# Project Name

## What it does
Clear, one-sentence description

## Why it exists
Problem it solves

## How to use it
Quick start guide

## Where to learn more
Links to detailed docs
```

### 2. Changelog Format
```markdown
# Changelog

## [1.2.0] - 2024-01-15

### Added
- New feature X
- Support for Y

### Changed
- Improved performance of Z
- Updated dependency A to v2.0

### Fixed
- Bug in feature B
- Security issue in C

### Deprecated
- Old API endpoint /v1/users

### Removed
- Support for Node.js 14

## [1.1.0] - 2023-12-01
...
```

### 3. Contributing Guide
```markdown
# Contributing

## Getting Started

1. Fork the repository
2. Clone your fork
3. Create a feature branch
4. Make your changes
5. Write tests
6. Submit a pull request

## Development Setup

\`\`\`bash
npm install
npm run dev
\`\`\`

## Running Tests

\`\`\`bash
npm test
\`\`\`

## Code Style

- Follow ESLint rules
- Use Prettier for formatting
- Write meaningful commit messages

## Pull Request Process

1. Update documentation
2. Add tests for new features
3. Ensure all tests pass
4. Update CHANGELOG.md
5. Request review from maintainers
```

### 4. JSDoc Standards
```typescript
/**
 * User account information.
 */
interface User {
  /** Unique user identifier */
  id: string;
  /** User's full name */
  name: string;
  /** User's email address */
  email: string;
  /** Account creation timestamp */
  createdAt: Date;
}

/**
 * Creates a new user account.
 * 
 * @param data - User registration data
 * @param data.name - User's full name
 * @param data.email - User's email address
 * @param data.password - User's password (will be hashed)
 * @returns Promise resolving to created user
 * @throws {ValidationError} If data is invalid
 * @throws {ConflictError} If email already exists
 * 
 * @example
 * ```typescript
 * const user = await createUser({
 *   name: 'John Doe',
 *   email: 'john@example.com',
 *   password: 'securePassword123'
 * });
 * ```
 */
async function createUser(data: CreateUserData): Promise<User> {
  // Implementation
}
```

### 5. Architecture Documentation
```markdown
# Architecture

## Overview
High-level system architecture diagram and description.

## Components

### Frontend
- React application
- State management with Redux
- Routing with React Router

### Backend
- Node.js/Express API
- PostgreSQL database
- Redis cache

### Infrastructure
- AWS hosting
- CloudFront CDN
- S3 for static assets

## Data Flow

1. User makes request
2. Frontend sends API call
3. Backend validates request
4. Database query executed
5. Response returned to frontend
6. UI updated

## Security
- JWT authentication
- HTTPS only
- Rate limiting
- Input validation
```

## Documentation Types

### 1. Code Documentation
- Inline comments for complex logic
- JSDoc for functions and classes
- Type definitions with descriptions

### 2. API Documentation
- Endpoint descriptions
- Request/response examples
- Error codes and messages
- Authentication requirements

### 3. User Documentation
- Getting started guides
- Tutorials and examples
- FAQ section
- Troubleshooting guide

### 4. Developer Documentation
- Setup instructions
- Architecture overview
- Contributing guidelines
- Testing procedures

## Common Pitfalls

### Pitfall 1: Over-Commenting
```typescript
// ❌ Obvious comments
// Increment counter by 1
counter++;

// ✅ Explain why, not what
// Reset counter after batch processing completes
counter = 0;
```

### Pitfall 2: No Examples
```markdown
❌ Avoid
## Usage
Call the function with parameters.

✅ Better
## Usage
\`\`\`typescript
import { processData } from 'package';

const result = processData({
  input: 'data',
  options: { format: 'json' }
});
\`\`\`
```

### Pitfall 3: Missing Context
```markdown
❌ Avoid
## Error Codes
- 1001: Error
- 1002: Error

✅ Better
## Error Codes
- `1001`: Invalid input format - Check data structure
- `1002`: Database connection failed - Verify credentials
```

## Documentation Checklist

- [ ] README with clear description and examples
- [ ] Installation instructions
- [ ] Quick start guide
- [ ] API reference with examples
- [ ] Contributing guidelines
- [ ] Changelog maintained
- [ ] Code comments for complex logic
- [ ] JSDoc for public APIs
- [ ] Error messages are helpful
- [ ] Examples are tested and working

## Tools

- **JSDoc**: JavaScript documentation generator
- **TypeDoc**: TypeScript documentation generator
- **Swagger/OpenAPI**: API documentation
- **Docusaurus**: Documentation websites
- **Storybook**: Component documentation

## References
- [Write the Docs](https://www.writethedocs.org/)
- [Google Developer Documentation Style Guide](https://developers.google.com/style)
- [JSDoc Reference](https://jsdoc.app/)

## Related Rules
- [API Design Principles](../backend/api-design-principles.md)
- [TypeScript Standards](../web/typescript-standards.md)
