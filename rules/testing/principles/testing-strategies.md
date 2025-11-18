# Testing Strategies

## Objective
Establish comprehensive testing practices for reliable, maintainable software across all layers.

## Context
Apply when:
- Writing unit, integration, and E2E tests
- Setting up test infrastructure
- Implementing test automation
- Defining testing standards for teams

## Guidelines

### Core Principles

1. **Test Pyramid**: More unit tests, fewer integration tests, minimal E2E tests
2. **Test Behavior, Not Implementation**: Focus on what code does, not how
3. **Arrange-Act-Assert**: Structure tests clearly
4. **Independent Tests**: Each test should run in isolation
5. **Fast Feedback**: Tests should run quickly

### Do This ✅

**Pattern 1: Unit Testing**
```typescript
// Testing a pure function
describe('calculateTotal', () => {
  it('should calculate total with tax', () => {
    // Arrange
    const items = [
      { price: 10, quantity: 2 },
      { price: 5, quantity: 3 }
    ];
    const taxRate = 0.1;

    // Act
    const result = calculateTotal(items, taxRate);

    // Assert
    expect(result).toBe(38.5); // (20 + 15) * 1.1
  });

  it('should handle empty items', () => {
    expect(calculateTotal([], 0.1)).toBe(0);
  });

  it('should handle zero tax rate', () => {
    const items = [{ price: 10, quantity: 1 }];
    expect(calculateTotal(items, 0)).toBe(10);
  });
});
```

**Pattern 2: Component Testing (React)**
```typescript
import { render, screen, fireEvent } from '@testing-library/react';
import { LoginForm } from './LoginForm';

describe('LoginForm', () => {
  it('should submit form with valid credentials', async () => {
    const onSubmit = jest.fn();
    render(<LoginForm onSubmit={onSubmit} />);

    // Fill form
    fireEvent.change(screen.getByLabelText(/email/i), {
      target: { value: 'user@example.com' }
    });
    fireEvent.change(screen.getByLabelText(/password/i), {
      target: { value: 'password123' }
    });

    // Submit
    fireEvent.click(screen.getByRole('button', { name: /login/i }));

    // Assert
    expect(onSubmit).toHaveBeenCalledWith({
      email: 'user@example.com',
      password: 'password123'
    });
  });

  it('should display validation errors', async () => {
    render(<LoginForm onSubmit={jest.fn()} />);

    // Submit without filling
    fireEvent.click(screen.getByRole('button', { name: /login/i }));

    // Assert errors appear
    expect(await screen.findByText(/email is required/i)).toBeInTheDocument();
    expect(await screen.findByText(/password is required/i)).toBeInTheDocument();
  });
});
```

**Pattern 3: API Testing**
```typescript
describe('User API', () => {
  beforeEach(async () => {
    await db.clear();
  });

  describe('POST /api/users', () => {
    it('should create a new user', async () => {
      const userData = {
        name: 'John Doe',
        email: 'john@example.com',
        password: 'password123'
      };

      const response = await request(app)
        .post('/api/users')
        .send(userData)
        .expect(201);

      expect(response.body).toMatchObject({
        success: true,
        data: {
          name: userData.name,
          email: userData.email
        }
      });
      expect(response.body.data.password).toBeUndefined();
    });

    it('should return 409 for duplicate email', async () => {
      const userData = {
        name: 'John Doe',
        email: 'john@example.com',
        password: 'password123'
      };

      // Create first user
      await request(app).post('/api/users').send(userData);

      // Try to create duplicate
      const response = await request(app)
        .post('/api/users')
        .send(userData)
        .expect(409);

      expect(response.body.error.code).toBe('CONFLICT');
    });
  });
});
```

### Avoid This ❌

**Anti-pattern 1: Testing Implementation Details**
```typescript
// ❌ Avoid - testing internal state
it('should set loading to true', () => {
  const component = render(<UserList />);
  expect(component.state.loading).toBe(true);
});

// ✅ Better - test user-visible behavior
it('should show loading indicator', () => {
  render(<UserList />);
  expect(screen.getByText(/loading/i)).toBeInTheDocument();
});
```

**Anti-pattern 2: Dependent Tests**
```typescript
// ❌ Avoid - tests depend on each other
describe('User flow', () => {
  let userId;

  it('should create user', async () => {
    const user = await createUser();
    userId = user.id; // Shared state
  });

  it('should update user', async () => {
    await updateUser(userId); // Depends on previous test
  });
});

// ✅ Better - independent tests
describe('User flow', () => {
  it('should create user', async () => {
    const user = await createUser();
    expect(user.id).toBeDefined();
  });

  it('should update user', async () => {
    const user = await createUser(); // Create fresh user
    const updated = await updateUser(user.id);
    expect(updated.name).toBe('Updated Name');
  });
});
```

## Best Practices

### 1. Test Coverage Goals
```
Unit Tests:        70-80% coverage
Integration Tests: Key workflows
E2E Tests:         Critical user paths
```

### 2. Mocking Strategy
```typescript
// Mock external dependencies
jest.mock('./api', () => ({
  fetchUser: jest.fn()
}));

// Use mock in test
it('should handle API error', async () => {
  const { fetchUser } = require('./api');
  fetchUser.mockRejectedValue(new Error('API Error'));

  render(<UserProfile userId="123" />);

  expect(await screen.findByText(/error/i)).toBeInTheDocument();
});
```

### 3. Test Data Factories
```typescript
// Create reusable test data
const createUser = (overrides = {}) => ({
  id: '123',
  name: 'John Doe',
  email: 'john@example.com',
  role: 'user',
  ...overrides
});

// Use in tests
it('should display admin badge', () => {
  const admin = createUser({ role: 'admin' });
  render(<UserCard user={admin} />);
  expect(screen.getByText(/admin/i)).toBeInTheDocument();
});
```

### 4. Async Testing
```typescript
// Wait for async operations
it('should load user data', async () => {
  render(<UserProfile userId="123" />);

  // Wait for loading to finish
  await waitFor(() => {
    expect(screen.queryByText(/loading/i)).not.toBeInTheDocument();
  });

  // Assert data is displayed
  expect(screen.getByText('John Doe')).toBeInTheDocument();
});
```

### 5. Snapshot Testing (Use Sparingly)
```typescript
// Only for stable, simple components
it('should match snapshot', () => {
  const { container } = render(<Button>Click me</Button>);
  expect(container.firstChild).toMatchSnapshot();
});
```

## Testing Pyramid

```
        /\
       /  \      E2E Tests (5%)
      /    \     - Critical user flows
     /------\    - Smoke tests
    /        \   
   /          \  Integration Tests (15%)
  /            \ - API endpoints
 /              \- Component integration
/----------------\
|                | Unit Tests (80%)
|                | - Pure functions
|                | - Components
|                | - Utilities
------------------
```

## Common Pitfalls

### Pitfall 1: Over-Mocking
```typescript
// ❌ Avoid - mocking everything
jest.mock('./utils');
jest.mock('./api');
jest.mock('./helpers');
// Test becomes meaningless

// ✅ Better - mock only external dependencies
jest.mock('./api'); // External API
// Test actual utils and helpers
```

### Pitfall 2: Flaky Tests
```typescript
// ❌ Avoid - timing-dependent tests
it('should update after 1 second', (done) => {
  setTimeout(() => {
    expect(value).toBe(10);
    done();
  }, 1000);
});

// ✅ Better - use proper async utilities
it('should update value', async () => {
  await waitFor(() => {
    expect(value).toBe(10);
  });
});
```

### Pitfall 3: Testing Too Much
```typescript
// ❌ Avoid - testing library code
it('should call useState', () => {
  // Testing React internals
});

// ✅ Better - test your code's behavior
it('should update count when button clicked', () => {
  // Test your component's behavior
});
```

## References
- [Testing Library](https://testing-library.com/)
- [Jest Documentation](https://jestjs.io/)
- [Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html)

## Related Rules
- [React Best Practices](../web/react-best-practices.md)
- [API Design Principles](../backend/api-design-principles.md)
