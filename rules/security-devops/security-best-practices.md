# Security Best Practices

## Objective
Establish security standards to protect applications from common vulnerabilities and threats.

## Context
Apply when:
- Handling user authentication and authorization
- Processing sensitive data
- Implementing API security
- Deploying applications to production

## Guidelines

### Core Principles

1. **Defense in Depth**: Multiple layers of security
2. **Least Privilege**: Minimum necessary permissions
3. **Fail Securely**: Secure defaults, fail closed
4. **Never Trust Input**: Validate and sanitize all input
5. **Keep Secrets Secret**: Never expose credentials

### Do This ✅

**Pattern 1: Password Security**
```typescript
import bcrypt from 'bcrypt';

// Hash passwords before storing
async function hashPassword(password: string): Promise<string> {
  const saltRounds = 12;
  return bcrypt.hash(password, saltRounds);
}

// Verify passwords
async function verifyPassword(
  password: string,
  hash: string
): Promise<boolean> {
  return bcrypt.compare(password, hash);
}

// Password requirements
function validatePassword(password: string): boolean {
  return (
    password.length >= 12 &&
    /[A-Z]/.test(password) &&
    /[a-z]/.test(password) &&
    /[0-9]/.test(password) &&
    /[^A-Za-z0-9]/.test(password)
  );
}
```

**Pattern 2: JWT Authentication**
```typescript
import jwt from 'jsonwebtoken';

// Generate token
function generateToken(userId: string): string {
  return jwt.sign(
    { userId },
    process.env.JWT_SECRET!,
    { expiresIn: '1h' }
  );
}

// Verify token middleware
function authenticateToken(req, res, next) {
  const token = req.headers.authorization?.split(' ')[1];

  if (!token) {
    return res.status(401).json({
      success: false,
      error: { code: 'UNAUTHORIZED', message: 'No token provided' }
    });
  }

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET!);
    req.user = decoded;
    next();
  } catch (error) {
    return res.status(401).json({
      success: false,
      error: { code: 'UNAUTHORIZED', message: 'Invalid token' }
    });
  }
}
```

**Pattern 3: Input Validation**
```typescript
import { z } from 'zod';

// Define schema
const userSchema = z.object({
  email: z.string().email(),
  name: z.string().min(2).max(100),
  age: z.number().int().min(18).max(120)
});

// Validate input
function validateUser(data: unknown) {
  try {
    return userSchema.parse(data);
  } catch (error) {
    throw new ValidationError('Invalid user data', error);
  }
}

// SQL injection prevention
function getUserById(id: string) {
  // ✅ Use parameterized queries
  return db.query('SELECT * FROM users WHERE id = $1', [id]);
  
  // ❌ Never concatenate SQL
  // return db.query(`SELECT * FROM users WHERE id = '${id}'`);
}
```

### Avoid This ❌

**Anti-pattern 1: Storing Plain Text Passwords**
```typescript
// ❌ Never store plain text passwords
const user = {
  email: 'user@example.com',
  password: 'password123' // Plain text!
};

// ✅ Always hash passwords
const user = {
  email: 'user@example.com',
  password: await hashPassword('password123')
};
```

**Anti-pattern 2: Exposing Sensitive Data**
```typescript
// ❌ Avoid exposing sensitive data
app.get('/api/users/:id', async (req, res) => {
  const user = await User.findById(req.params.id);
  res.json(user); // Includes password hash!
});

// ✅ Exclude sensitive fields
app.get('/api/users/:id', async (req, res) => {
  const user = await User.findById(req.params.id);
  const { password, ...safeUser } = user;
  res.json(safeUser);
});
```

## Best Practices

### 1. Environment Variables
```typescript
// .env file (never commit!)
DATABASE_URL=postgresql://localhost:5432/mydb
JWT_SECRET=your-secret-key-here
API_KEY=your-api-key-here

// Load in application
import dotenv from 'dotenv';
dotenv.config();

const config = {
  database: process.env.DATABASE_URL,
  jwtSecret: process.env.JWT_SECRET,
  apiKey: process.env.API_KEY
};

// Validate required env vars
if (!config.jwtSecret) {
  throw new Error('JWT_SECRET is required');
}
```

### 2. CORS Configuration
```typescript
import cors from 'cors';

// ❌ Avoid - allows all origins
app.use(cors());

// ✅ Better - specific origins
app.use(cors({
  origin: process.env.ALLOWED_ORIGINS?.split(',') || ['http://localhost:3000'],
  credentials: true,
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization']
}));
```

### 3. Rate Limiting
```typescript
import rateLimit from 'express-rate-limit';

// API rate limiting
const apiLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // Limit each IP to 100 requests per windowMs
  message: 'Too many requests from this IP'
});

app.use('/api/', apiLimiter);

// Stricter limit for auth endpoints
const authLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 5,
  message: 'Too many login attempts'
});

app.use('/api/auth/', authLimiter);
```

### 4. HTTPS Only
```typescript
// Redirect HTTP to HTTPS
app.use((req, res, next) => {
  if (req.header('x-forwarded-proto') !== 'https' && process.env.NODE_ENV === 'production') {
    res.redirect(`https://${req.header('host')}${req.url}`);
  } else {
    next();
  }
});

// Set security headers
import helmet from 'helmet';
app.use(helmet());
```

### 5. XSS Prevention
```typescript
// Sanitize HTML input
import DOMPurify from 'isomorphic-dompurify';

function sanitizeHtml(dirty: string): string {
  return DOMPurify.sanitize(dirty, {
    ALLOWED_TAGS: ['b', 'i', 'em', 'strong', 'a'],
    ALLOWED_ATTR: ['href']
  });
}

// Escape output in templates
// Use templating engines that auto-escape (React, Vue, etc.)
```

### 6. CSRF Protection
```typescript
import csrf from 'csurf';

// Enable CSRF protection
const csrfProtection = csrf({ cookie: true });

app.post('/api/transfer', csrfProtection, (req, res) => {
  // Protected endpoint
});

// Send CSRF token to client
app.get('/api/csrf-token', csrfProtection, (req, res) => {
  res.json({ csrfToken: req.csrfToken() });
});
```

### 7. Secure Session Management
```typescript
import session from 'express-session';

app.use(session({
  secret: process.env.SESSION_SECRET!,
  resave: false,
  saveUninitialized: false,
  cookie: {
    secure: process.env.NODE_ENV === 'production', // HTTPS only
    httpOnly: true, // Prevent XSS
    maxAge: 24 * 60 * 60 * 1000, // 24 hours
    sameSite: 'strict' // CSRF protection
  }
}));
```

## OWASP Top 10 Protection

### 1. Injection
```typescript
// ✅ Use parameterized queries
db.query('SELECT * FROM users WHERE email = $1', [email]);

// ✅ Use ORMs with built-in protection
User.findOne({ where: { email } });
```

### 2. Broken Authentication
```typescript
// ✅ Implement MFA
// ✅ Use secure session management
// ✅ Implement account lockout
// ✅ Use strong password policies
```

### 3. Sensitive Data Exposure
```typescript
// ✅ Encrypt data at rest
// ✅ Use HTTPS for data in transit
// ✅ Don't log sensitive data
// ✅ Implement proper access controls
```

### 4. XML External Entities (XXE)
```typescript
// ✅ Disable XML external entity processing
// ✅ Use JSON instead of XML when possible
```

### 5. Broken Access Control
```typescript
// ✅ Implement proper authorization checks
function checkOwnership(req, res, next) {
  const resource = await Resource.findById(req.params.id);
  if (resource.userId !== req.user.id) {
    return res.status(403).json({
      success: false,
      error: { code: 'FORBIDDEN', message: 'Access denied' }
    });
  }
  next();
}
```

## Common Pitfalls

### Pitfall 1: Trusting Client-Side Validation
```typescript
// ❌ Only client-side validation
// User can bypass this

// ✅ Always validate on server
app.post('/api/users', (req, res) => {
  const validation = validateUser(req.body);
  if (!validation.success) {
    return res.status(400).json({ error: validation.error });
  }
  // Proceed with validated data
});
```

### Pitfall 2: Logging Sensitive Data
```typescript
// ❌ Avoid logging sensitive data
console.log('User login:', { email, password });

// ✅ Log safely
console.log('User login attempt:', { email });
```

### Pitfall 3: Using Weak Cryptography
```typescript
// ❌ Avoid weak algorithms
const hash = crypto.createHash('md5').update(password).digest('hex');

// ✅ Use strong algorithms
const hash = await bcrypt.hash(password, 12);
```

## Security Checklist

- [ ] All passwords are hashed with bcrypt/argon2
- [ ] JWT tokens have expiration times
- [ ] Environment variables are used for secrets
- [ ] HTTPS is enforced in production
- [ ] CORS is properly configured
- [ ] Rate limiting is implemented
- [ ] Input validation is performed server-side
- [ ] SQL injection is prevented with parameterized queries
- [ ] XSS protection is enabled
- [ ] CSRF protection is implemented
- [ ] Security headers are set (helmet.js)
- [ ] Sensitive data is not logged
- [ ] Dependencies are regularly updated
- [ ] Security audits are performed (npm audit)

## References
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)
- [Node.js Security Best Practices](https://nodejs.org/en/docs/guides/security/)

## Related Rules
- [API Design Principles](../backend/api-design-principles.md)
- [TypeScript Standards](../web/typescript-standards.md)
