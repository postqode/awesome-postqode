## Brief overview

This rule defines best practices for Vue.js development using modern Vue 3 with Composition API. It emphasizes reactive programming patterns, component architecture, and performance optimization for building scalable Vue applications.

## Component architecture and design

- Use single-file components (.vue files) for encapsulated functionality
- Implement Composition API with setup() script for better logic organization
- Use script setup syntax for cleaner and more concise component code
- Create reusable components with proper props and emits interfaces
- Implement proper component lifecycle management with onMounted, onUnmounted
- Use computed properties for derived state and memoization
- Implement watchers for side effects and reactive dependencies
- Design components with single responsibility principle

## Reactivity and state management

- Use ref() for primitive values and reactive() for objects
- Implement computed properties for derived state calculations
- Use watch() and watchEffect() for side effects and dependencies
- Leverage Vue's reactivity system instead of manual DOM manipulation
- Use provide/inject for dependency injection across component trees
- Implement proper state management patterns for complex applications
- Use shallow ref for performance optimization in large lists
- Implement immutable state updates for predictable reactivity

## TypeScript integration

- Use TypeScript with proper type definitions for props, emits, and refs
- Define interfaces for component props and emitted events
- Use generic types for reusable components
- Implement proper type inference with Vue's built-in utilities
- Use type-safe event handling and method signatures
- Implement proper typing for composition functions
- Use Vue's built-in type definitions and augment when needed
- Create custom type definitions for plugin integrations

## Performance optimization

- Use v-memo for expensive components and prevent unnecessary re-renders
- Implement virtual scrolling for large lists with vue-virtual-scroller
- Use lazy loading for components and routes with defineAsyncComponent
- Implement proper key attributes for efficient list rendering
- Use computed properties instead of methods in templates
- Implement code splitting with dynamic imports
- Use v-show vs v-if appropriately for conditional rendering
- Implement proper image optimization and lazy loading

## Routing and navigation

- Use Vue Router with proper route definitions and guards
- Implement nested routes for complex application structures
- Use route parameters and query parameters effectively
- Implement proper navigation guards for authentication and authorization
- Use programmatic navigation with router.push() and router.replace()
- Implement breadcrumb navigation and route meta information
- Use lazy-loaded routes for better initial load performance

## Form handling and validation

- Use v-model with proper modifiers (.lazy, .number, .trim)
- Implement form validation with computed properties and watchers
- Use composition functions for reusable form logic
- Implement proper error handling and validation messages
- Use form submission handling with proper loading states
- Implement custom validators and async validation
- Use proper form reset and initialization patterns

## Styling and CSS integration

- Use scoped styles for component-specific styling
- Implement CSS modules or utility-first CSS approaches
- Use CSS variables for theming and dynamic styling
- Implement responsive design with proper breakpoints
- Use transition and animation components for smooth UX
- Implement proper CSS organization and architecture
- Use utility classes for common styling patterns

## Testing strategies

- Use Vue Test Utils for component unit testing
- Implement proper component mounting and prop passing in tests
- Use mocking for external dependencies and API calls
- Test component reactivity and state changes
- Implement integration testing with Cypress or Playwright
- Test component lifecycle hooks and side effects
- Use snapshot testing for UI consistency
- Implement accessibility testing in component tests

## Pinia store management

- Use Pinia for state management in larger applications
- Implement stores with proper state, getters, and actions
- Use composition API style stores with setup() function
- Implement proper store organization by feature or domain
- Use store composition for complex state scenarios
- Implement proper TypeScript typing for stores
- Use store persistence and hydration strategies
- Implement proper error handling in store actions

## Plugin and ecosystem integration

- Use Vue CLI for project scaffolding and development
- Implement proper plugin configuration and usage
- Use Vite for modern build tooling and development server
- Integrate with popular libraries (VueUse, Vue Router, Pinia)
- Implement proper build configuration and optimization
- Use environment-specific configurations
- Implement proper dependency management and updates

## Code organization and best practices

- Use composition functions for reusable logic
- Implement proper file and folder structure
- Use consistent naming conventions for components and utilities
- Implement proper import/export patterns
- Use ESLint and Prettier for code consistency
- Implement proper error handling and logging
- Use semantic HTML and accessibility best practices
- Implement proper documentation and commenting

## Development workflow

- Use Vue DevTools for debugging and inspection
- Implement hot module replacement for efficient development
- Use proper build configuration for different environments
- Implement proper source maps and debugging setup
- Use component documentation with JSDoc or Vue-specific formats
- Implement proper Git workflow and branching strategies
- Use continuous integration and deployment pipelines

## Security best practices

- Implement proper input sanitization and validation
- Use Content Security Policy headers in production
- Implement proper authentication and authorization patterns
- Use HTTPS and secure cookie handling
- Implement XSS protection and output encoding
- Use proper CSRF protection for form submissions
- Implement secure API communication practices
