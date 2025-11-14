## Brief overview

This rule defines best practices for Angular development using modern Angular features. It emphasizes proper component architecture, reactive programming patterns, and TypeScript integration for building scalable Angular applications.

## Component architecture and design

- Use standalone components with proper encapsulation
- Implement proper component lifecycle hooks (ngOnInit, ngOnDestroy, etc.)
- Use proper input/output properties with @Input() and @Output() decorators
- Implement proper change detection with OnChanges interface
- Use proper component communication with services and events
- Design components with single responsibility principle
- Use proper component styling with encapsulated styles
- Implement proper component testing with TestBed
- Use proper lazy loading and onPush change detection strategies

## Reactive programming and RxJS

- Use RxJS operators for data transformation and filtering
- Implement proper subscription management with takeUntil and unsubscribe
- Use proper async pipe patterns for data processing
- Implement proper error handling in reactive streams
- Use proper subject/behavior patterns for component communication
- Implement proper hot observable patterns for real-time data
- Use proper backpressure handling in high-frequency streams
- Implement proper reactive form handling with valueChanges and statusChanges

## Services and dependency injection

- Use Angular's dependency injection system with @Injectable()
- Implement proper service architecture with separation of concerns
- Use proper providedIn metadata for tree-shaking optimization
- Implement proper singleton and state management services
- Use proper HTTP client with HttpClient and interceptors
- Implement proper error handling and retry logic in services
- Use proper service testing with HttpClientTestingModule
- Implement proper caching and data management services

## Routing and navigation

- Use Angular Router with proper route configuration
- Implement proper route guards for authentication and authorization
- Use proper lazy loading modules with loadChildren
- Implement proper route parameters and query handling
- Use proper navigation events and router state management
- Implement proper breadcrumb and navigation history
- Use proper route resolvers and data pre-fetching
- Implement proper nested routing and child routes

## Forms and validation

- Use Angular Reactive Forms with proper form controls
- Implement proper form validation with custom validators
- Use proper form groups and nested forms
- Implement proper async validation with async validators
- Use proper form submission and error handling
- Implement proper form arrays and dynamic forms
- Use proper form testing with ReactiveFormsModule
- Implement proper cross-field validation and conditional validation

## TypeScript integration

- Use strict TypeScript configuration with proper compiler options
- Implement proper interface definitions for components and services
- Use proper generic types for reusable components
- Implement proper type guards and type assertions
- Use proper service typing with HttpClient and observables
- Implement proper event typing and custom event types
- Use proper module declaration and barrel exports
- Implement proper typing for RxJS operators and observables

## Performance optimization

- Use OnPush change detection with proper comparison strategies
- Implement proper trackBy functions for efficient change detection
- Use proper lazy loading and code splitting strategies
- Implement proper memoization with pure pipes and memoized functions
- Use proper virtual scrolling for large lists
- Implement proper zone.js integration for change detection optimization
- Use proper AOT compilation for production builds
- Implement proper bundle analysis and optimization
- Use proper differential loading for efficient updates

## Testing strategies

- Use Angular's testing utilities with TestBed and ComponentFixture
- Implement proper unit testing with services and HTTP mocking
- Use proper integration testing with RouterTestingModule
- Implement proper end-to-end testing with Protractor or Cypress
- Use proper component testing with shallow rendering
- Implement proper form testing with FormControl and ReactiveFormsModule
- Use proper mocking strategies for services and dependencies
- Implement proper test data management with fixtures and factories

## State management

- Use proper NgRx or NgRx for complex state management
- Implement proper store architecture with actions, reducers, and selectors
- Use proper state persistence and hydration strategies
- Implement proper state synchronization across components
- Use proper state debugging and devtools integration
- Implement proper state testing with store mocking
- Use proper state normalization and normalization strategies
- Implement proper state history and undo/redo functionality

## Security best practices

- Implement proper authentication and authorization with Angular guards
- Use proper XSS protection and output sanitization
- Implement proper CSRF protection and secure headers
- Use proper route guards for protected routes
- Implement proper input validation and sanitization
- Use proper HTTPS and secure communication practices
- Implement proper content security policy headers
- Use proper dependency injection security and validation
- Implement proper audit logging and security monitoring

## Build and deployment

- Use Angular CLI for proper project scaffolding and building
- Implement proper environment configuration with environment.ts files
- Use proper AOT compilation for production builds
- Implement proper bundle optimization and tree-shaking
- Use proper deployment strategies with SSR and static hosting
- Implement proper CI/CD integration with Angular builds
- Use proper Docker containerization for deployment
- Implement proper progressive web app strategies

## Code organization and best practices

- Use proper Angular project structure with feature modules
- Implement proper module organization with barrels and index.ts files
- Use proper naming conventions for components, services, and directives
- Implement proper linting with TSLint and Angular ESLint rules
- Use proper code formatting with Prettier and Angular formatting
- Implement proper documentation with JSDoc and Angular doc comments
- Use proper Git workflow and branching strategies
- Implement proper code review and quality gates
