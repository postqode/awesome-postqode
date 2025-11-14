# API Design Principles

## Objective
Establish RESTful API design standards for consistent, maintainable, and developer-friendly APIs.

## Context
Apply when:
- Designing REST APIs
- Creating API endpoints
- Defining request/response formats
- Implementing API versioning and documentation

## Guidelines

### Core Principles

1. **RESTful Design**: Follow REST architectural constraints
2. **Consistency**: Maintain consistent patterns across all endpoints
3. **Clear Naming**: Use intuitive, descriptive resource names
4. **Proper HTTP Methods**: Use correct HTTP verbs for operations
5. **Meaningful Status Codes**: Return appropriate HTTP status codes

### Do This ✅

**Pattern 1: Resource-Based URLs**
```
✅ Good - Resource-oriented
GET    /api/users              # Get all users
GET    /api/users/:id          # Get specific user
POST   /api/users              # Create user
PUT    /api/users/:id          # Update user (full)
PATCH  /api/users/:id          # Update user (partial)
DELETE /api/users/:id          # Delete user

GET    /api/users/:id/posts    # Get user's posts
POST   /api/users/:id/posts    # Create post for user
```

**Pattern 2: Standard Response Format**
```typescript
// Success response
interface SuccessResponse<T> {
  success: true;
  data: T;
  meta?: {
    page?: number;
    limit?: number;
    total?: number;
  };
}

// Error response
interface ErrorResponse {
  success: false;
  error: {
    code: string;
    message: string;
    details?: unknown;
  };
}

// Example responses
{
  "success": true,
  "data": {
    "id": "123",
    "name": "John Doe",
    "email": "john@example.com"
  }
}

{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid email format",
    "details": {
      "field": "email",
      "value": "invalid-email"
    }
  }
}
```

**Pattern 3: Proper HTTP Status Codes**
```typescript
// Success codes
200 OK              // Successful GET, PUT, PATCH, DELETE
201 Created         // Successful POST
204 No Content      // Successful DELETE with no response body

// Client error codes
400 Bad Request     // Invalid request format
401 Unauthorized    // Missing or invalid authentication
403 Forbidden       // Authenticated but not authorized
404 Not Found       // Resource doesn't exist
409 Conflict        // Resource conflict (e.g., duplicate)
422 Unprocessable   // Validation errors

// Server error codes
500 Internal Error  // Server error
503 Service Unavailable // Temporary unavailability
```

### Avoid This ❌

**Anti-pattern 1: Action-Based URLs**
```
❌ Avoid - Action-oriented
POST /api/createUser
POST /api/updateUser
POST /api/deleteUser
GET  /api/getUserById?id=123

✅ Use - Resource-oriented
POST   /api/users
PUT    /api/users/:id
DELETE /api/users/:id
GET    /api/users/:id
```

**Anti-pattern 2: Inconsistent Response Formats**
```typescript
// ❌ Avoid - Inconsistent
// Endpoint 1
{ "user": { "id": 1 } }

// Endpoint 2
{ "data": { "id": 1 } }

// Endpoint 3
{ "id": 1 }

// ✅ Use - Consistent
// All endpoints
{ "success": true, "data": { "id": 1 } }
```

## Best Practices

### 1. API Versioning
```
# URL versioning (recommended for major changes)
/api/v1/users
/api/v2/users

# Header versioning (for minor changes)
Accept: application/vnd.api+json; version=1
```

### 2. Pagination
```typescript
// Query parameters
GET /api/users?page=1&limit=20

// Response with pagination meta
{
  "success": true,
  "data": [...],
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 100,
    "totalPages": 5
  }
}
```

### 3. Filtering and Sorting
```
# Filtering
GET /api/users?role=admin&status=active

# Sorting
GET /api/users?sort=createdAt:desc

# Combined
GET /api/users?role=admin&sort=name:asc&page=1&limit=20
```

### 4. Field Selection
```
# Select specific fields
GET /api/users?fields=id,name,email

# Response
{
  "success": true,
  "data": [
    { "id": "1", "name": "John", "email": "john@example.com" }
  ]
}
```

### 5. Error Handling
```typescript
// Validation errors
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": [
      {
        "field": "email",
        "message": "Email is required"
      },
      {
        "field": "password",
        "message": "Password must be at least 8 characters"
      }
    ]
  }
}

// Not found error
{
  "success": false,
  "error": {
    "code": "NOT_FOUND",
    "message": "User not found",
    "details": {
      "resource": "user",
      "id": "123"
    }
  }
}
```

### 6. Authentication
```typescript
// JWT Bearer token
Authorization: Bearer <token>

// API Key
X-API-Key: <api-key>

// Response for unauthorized
{
  "success": false,
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Invalid or expired token"
  }
}
```

### 7. Rate Limiting
```
# Response headers
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640000000

# Rate limit exceeded response
HTTP 429 Too Many Requests
{
  "success": false,
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Too many requests",
    "details": {
      "retryAfter": 60
    }
  }
}
```

## Implementation Example

```typescript
// Express.js example
import express from 'express';

const router = express.Router();

// GET /api/users
router.get('/users', async (req, res) => {
  try {
    const { page = 1, limit = 20, sort, ...filters } = req.query;
    
    const users = await User.find(filters)
      .sort(sort)
      .skip((page - 1) * limit)
      .limit(limit);
    
    const total = await User.countDocuments(filters);
    
    res.json({
      success: true,
      data: users,
      meta: {
        page: Number(page),
        limit: Number(limit),
        total,
        totalPages: Math.ceil(total / limit)
      }
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: {
        code: 'INTERNAL_ERROR',
        message: 'Failed to fetch users'
      }
    });
  }
});

// POST /api/users
router.post('/users', async (req, res) => {
  try {
    const { email, name, password } = req.body;
    
    // Validation
    if (!email || !name || !password) {
      return res.status(400).json({
        success: false,
        error: {
          code: 'VALIDATION_ERROR',
          message: 'Missing required fields',
          details: {
            required: ['email', 'name', 'password']
          }
        }
      });
    }
    
    // Check for existing user
    const existing = await User.findOne({ email });
    if (existing) {
      return res.status(409).json({
        success: false,
        error: {
          code: 'CONFLICT',
          message: 'User already exists',
          details: { email }
        }
      });
    }
    
    const user = await User.create({ email, name, password });
    
    res.status(201).json({
      success: true,
      data: user
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      error: {
        code: 'INTERNAL_ERROR',
        message: 'Failed to create user'
      }
    });
  }
});
```

## Documentation Standards

### OpenAPI/Swagger Example
```yaml
openapi: 3.0.0
info:
  title: User API
  version: 1.0.0

paths:
  /users:
    get:
      summary: Get all users
      parameters:
        - name: page
          in: query
          schema:
            type: integer
            default: 1
        - name: limit
          in: query
          schema:
            type: integer
            default: 20
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                  data:
                    type: array
                    items:
                      $ref: '#/components/schemas/User'
```

## Common Pitfalls

### Pitfall 1: Using GET for State-Changing Operations
```
❌ Avoid
GET /api/users/123/delete

✅ Use
DELETE /api/users/123
```

### Pitfall 2: Exposing Internal IDs
```typescript
// ❌ Avoid - exposing database IDs
{
  "id": 12345,
  "name": "John"
}

// ✅ Better - use UUIDs or obfuscated IDs
{
  "id": "usr_a1b2c3d4",
  "name": "John"
}
```

### Pitfall 3: Not Handling Partial Updates
```typescript
// ❌ Avoid - PUT requires all fields
PUT /api/users/123
{ "name": "John" } // Missing other required fields

// ✅ Use PATCH for partial updates
PATCH /api/users/123
{ "name": "John" } // Only update name
```

## References
- [REST API Design Best Practices](https://restfulapi.net/)
- [HTTP Status Codes](https://httpstatuses.com/)
- [OpenAPI Specification](https://swagger.io/specification/)

## Related Rules
- [TypeScript Standards](../web/typescript-standards.md)
- [Security Best Practices](../security-devops/security-best-practices.md)
