# TypeScript Standards

## Objective
Establish TypeScript best practices for type-safe, maintainable code across all projects.

## Context
Apply when:
- Writing TypeScript code in any project
- Defining types and interfaces
- Working with generics and utility types
- Configuring TypeScript compiler options

## Guidelines

### Core Principles

1. **Strict Mode Always**: Enable strict mode in tsconfig.json
2. **Explicit Types**: Prefer explicit type annotations over inference when it improves clarity
3. **No Any**: Avoid `any` type - use `unknown` or proper types
4. **Type Safety**: Leverage TypeScript's type system fully
5. **Consistent Naming**: Follow naming conventions for types and interfaces

### Do This ✅

**Pattern 1: Interface Definitions**
```typescript
// Use interfaces for object shapes
interface User {
  id: string;
  name: string;
  email: string;
  role: UserRole;
  createdAt: Date;
  updatedAt?: Date; // Optional property
}

// Use type for unions, intersections, primitives
type UserRole = 'admin' | 'user' | 'guest';
type UserId = string;
type UserWithTimestamps = User & {
  deletedAt?: Date;
};
```

**Pattern 2: Function Type Annotations**
```typescript
// Explicit parameter and return types
function createUser(
  name: string,
  email: string,
  role: UserRole = 'user'
): User {
  return {
    id: generateId(),
    name,
    email,
    role,
    createdAt: new Date(),
  };
}

// Arrow function with types
const updateUser = (
  id: string,
  updates: Partial<User>
): Promise<User> => {
  return api.updateUser(id, updates);
};
```

**Pattern 3: Generics for Reusability**
```typescript
// Generic function
function getById<T extends { id: string }>(
  items: T[],
  id: string
): T | undefined {
  return items.find(item => item.id === id);
}

// Generic interface
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

// Usage
const userResponse: ApiResponse<User> = await fetchUser();
const usersResponse: ApiResponse<User[]> = await fetchUsers();
```

### Avoid This ❌

**Anti-pattern 1: Using Any**
```typescript
// ❌ Avoid
function processData(data: any): any {
  return data.value;
}

// ✅ Correct
function processData<T extends { value: unknown }>(data: T): T['value'] {
  return data.value;
}
```

**Anti-pattern 2: Type Assertions Without Validation**
```typescript
// ❌ Avoid - unsafe assertion
const user = data as User;

// ✅ Correct - with validation
function isUser(data: unknown): data is User {
  return (
    typeof data === 'object' &&
    data !== null &&
    'id' in data &&
    'name' in data &&
    'email' in data
  );
}

const user = isUser(data) ? data : null;
```

## Best Practices

### 1. Type vs Interface
- Use `interface` for object shapes that may be extended
- Use `type` for unions, intersections, and primitives
- Be consistent within a project

### 2. Utility Types
```typescript
// Partial - make all properties optional
type PartialUser = Partial<User>;

// Pick - select specific properties
type UserPreview = Pick<User, 'id' | 'name'>;

// Omit - exclude specific properties
type UserWithoutTimestamps = Omit<User, 'createdAt' | 'updatedAt'>;

// Required - make all properties required
type RequiredUser = Required<User>;

// Readonly - make all properties readonly
type ImmutableUser = Readonly<User>;
```

### 3. Strict Null Checks
```typescript
// Enable strictNullChecks in tsconfig.json
function findUser(id: string): User | null {
  const user = users.find(u => u.id === id);
  return user ?? null;
}

// Handle null/undefined explicitly
const userName = user?.name ?? 'Anonymous';
```

### 4. Discriminated Unions
```typescript
type Success<T> = {
  status: 'success';
  data: T;
};

type Error = {
  status: 'error';
  message: string;
};

type Result<T> = Success<T> | Error;

function handleResult<T>(result: Result<T>): void {
  if (result.status === 'success') {
    console.log(result.data); // TypeScript knows data exists
  } else {
    console.error(result.message); // TypeScript knows message exists
  }
}
```

### 5. Type Guards
```typescript
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

function isArray<T>(value: unknown): value is T[] {
  return Array.isArray(value);
}

function hasProperty<K extends string>(
  obj: unknown,
  key: K
): obj is Record<K, unknown> {
  return typeof obj === 'object' && obj !== null && key in obj;
}
```

## TSConfig Recommendations

```json
{
  "compilerOptions": {
    "strict": true,
    "target": "ES2020",
    "module": "ESNext",
    "lib": ["ES2020", "DOM"],
    "moduleResolution": "node",
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true
  }
}
```

## Common Pitfalls

### Pitfall 1: Overusing Type Assertions
```typescript
// ❌ Avoid
const value = input as string;

// ✅ Better - validate first
if (typeof input === 'string') {
  const value = input;
}
```

### Pitfall 2: Not Using Unknown Instead of Any
```typescript
// ❌ Avoid
function parse(json: string): any {
  return JSON.parse(json);
}

// ✅ Correct
function parse(json: string): unknown {
  return JSON.parse(json);
}
```

### Pitfall 3: Ignoring Null/Undefined
```typescript
// ❌ Avoid
function getLength(str: string): number {
  return str.length; // Crashes if str is null/undefined
}

// ✅ Correct
function getLength(str: string | null | undefined): number {
  return str?.length ?? 0;
}
```

## References
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
- [Type Challenges](https://github.com/type-challenges/type-challenges)

## Related Rules
- [React Best Practices](./react-best-practices.md)
- [API Design Principles](../backend/api-design-principles.md)
