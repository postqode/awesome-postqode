## Brief overview

This rule defines best practices for Django web development using Python. It emphasizes proper project structure, ORM usage, security practices, and performance optimization for building scalable Django applications.

## Project structure and organization

- Use Django's recommended project structure with separate apps for different features
- Organize apps by business domain or functionality (users, products, orders)
- Create separate settings files for different environments (development, staging, production)
- Use Django's built-in project template as starting point
- Implement proper package structure with __init__.py files
- Separate static files, templates, and media files appropriately
- Use Django's manage.py commands for common administrative tasks

## Models and database design

- Use Django ORM for all database operations, avoid raw SQL queries
- Define clear model relationships with proper foreign keys and many-to-many fields
- Use model validation and clean() methods for data integrity
- Implement proper indexing for frequently queried fields
- Use Django migrations for all schema changes
- Create abstract base models for common fields and methods
- Use model managers for custom query sets and filtering
- Implement soft deletes instead of hard deletes when appropriate

## Views and URL routing

- Use class-based views (CBVs) for consistency and reusability
- Implement proper HTTP method handling in views (GET, POST, PUT, DELETE)
- Use Django's URL patterns with named URLs for reverse routing
- Implement proper permission checks and authentication decorators
- Use viewsets and routers for API endpoints with Django REST Framework
- Create separate views for different HTTP methods when needed
- Use Django's built-in pagination for list views

## Templates and frontend integration

- Use Django template language with proper context variable passing
- Implement template inheritance with base templates for consistent layout
- Use template tags and filters for reusable UI components
- Separate static files (CSS, JS) from templates
- Use Django's static file serving in development, CDN in production
- Implement proper CSRF protection in forms
- Use Django forms for validation and cleaning user input

## Forms and validation

- Use Django forms for all user input handling and validation
- Implement custom form fields for complex input types
- Use formsets for handling multiple related forms
- Implement proper error handling and validation messages
- Use Django's built-in validators and create custom validators when needed
- Implement file upload handling with proper security checks
- Use form widgets for consistent UI components

## Security best practices

- Use Django's built-in authentication and authorization system
- Implement proper password hashing and user management
- Use Django's CSRF protection for all form submissions
- Implement proper permission checks for sensitive operations
- Use Django's security middleware for common vulnerabilities
- Validate and sanitize all user input
- Use HTTPS in production and implement proper headers
- Implement rate limiting for API endpoints

## API development with Django REST Framework

- Use serializers for proper data validation and response formatting
- Implement proper HTTP status codes and error handling
- Use viewsets and routers for standard CRUD operations
- Implement pagination, filtering, and ordering for list endpoints
- Use proper authentication and permission classes for API access
- Implement API versioning for backward compatibility
- Use throttling and rate limiting for API protection

## Performance optimization

- Use select_related and prefetch_related for database query optimization
- Implement proper database indexing for frequently accessed data
- Use Django's caching framework with appropriate cache backends
- Implement lazy loading for large datasets and file operations
- Use database connection pooling and proper transaction management
- Implement CDN for static files in production
- Use Django's debug toolbar for performance profiling in development

## Testing strategies

- Write unit tests for models, views, forms, and utilities
- Use Django's test client for integration testing
- Create fixtures for consistent test data
- Test database migrations and model relationships
- Implement API testing with Django REST Framework test client
- Use coverage reporting to ensure comprehensive test coverage
- Test security features and permission checks

## Configuration and deployment

- Use environment variables for sensitive configuration
- Implement proper logging configuration for different environments
- Use Django's settings module structure with separation of concerns
- Implement proper WSGI/ASGI configuration for production servers
- Use Docker containers for consistent deployment environments
- Implement proper database configuration for production use
- Use process managers like Gunicorn or uWSGI for production

## Middleware and utilities

- Create custom middleware for cross-cutting concerns
- Implement proper request logging and error tracking
- Use Django's built-in middleware for common functionality
- Create utility functions for common operations across apps
- Implement proper exception handling and error reporting
- Use context processors for global template variables
- Implement custom management commands for administrative tasks

## Internationalization and localization

- Use Django's i18n framework for multi-language support
- Implement proper translation files and message extraction
- Use timezone-aware datetime handling
- Implement locale-specific formatting for dates, numbers, and currency
- Use Django's translation functions in templates and code
- Test internationalization features thoroughly

## Admin interface customization

- Customize Django admin for better user experience
- Implement proper admin actions for bulk operations
- Use admin inlines for related model editing
- Implement proper search and filtering in admin interface
- Customize admin forms and validation when needed
- Use admin permissions to control access to sensitive features
