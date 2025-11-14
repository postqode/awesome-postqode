## Brief overview

This rule defines best practices for SQL database design, query optimization, and data management. It emphasizes proper schema design, indexing strategies, and performance optimization for scalable database applications.

## Schema design and normalization

- Use proper normalization (1NF, 2NF, 3NF) to reduce data redundancy
- Implement appropriate primary keys and foreign key relationships
- Use consistent naming conventions for tables, columns, and constraints
- Design for data integrity with proper constraints and validation rules
- Use appropriate data types to optimize storage and performance
- Implement proper relationship modeling (one-to-one, one-to-many, many-to-many)
- Use surrogate keys for complex composite primary keys
- Design for future scalability and extensibility

## Indexing and performance optimization

- Create indexes on frequently queried columns and foreign keys
- Use composite indexes for multi-column queries
- Implement proper covering indexes for complex queries
- Avoid over-indexing which impacts write performance
- Use partial indexes for specific query patterns
- Implement proper index maintenance and statistics updates
- Use query execution plans to identify performance bottlenecks
- Monitor index usage and remove unused indexes

## Query writing best practices

- Write explicit column names instead of SELECT *
- Use appropriate JOIN types (INNER, LEFT, RIGHT) for relationships
- Implement proper WHERE clauses to filter data early
- Avoid subqueries when JOINs would be more efficient
- Use appropriate aggregate functions (COUNT, SUM, AVG) with GROUP BY
- Implement proper pagination with LIMIT and OFFSET
- Use parameterized queries to prevent SQL injection
- Avoid cursors when set-based operations are possible

## Transaction management

- Use appropriate transaction isolation levels for consistency
- Keep transactions short and focused to reduce locking
- Implement proper error handling and rollback strategies
- Use savepoints for complex transaction management
- Implement proper deadlock detection and handling
- Use appropriate locking strategies for concurrent access
- Implement proper transaction logging and auditing
- Use optimistic locking for high-concurrency scenarios

## Data integrity and constraints

- Implement proper NOT NULL constraints for required fields
- Use CHECK constraints for data validation rules
- Implement UNIQUE constraints for duplicate prevention
- Use foreign key constraints for referential integrity
- Implement proper cascade rules for updates and deletes
- Use appropriate default values for data consistency
- Implement proper domain constraints for business rules
- Use triggers for complex data validation and auditing

## Database security

- Implement proper user authentication and authorization
- Use principle of least privilege for database access
- Implement proper data encryption for sensitive information
- Use parameterized queries to prevent SQL injection
- Implement proper audit logging for data access
- Use appropriate network security and firewall rules
- Implement proper backup and disaster recovery
- Use data masking for non-production environments

## Backup and recovery strategies

- Implement regular automated backup schedules
- Use appropriate backup types (full, incremental, differential)
- Implement proper backup verification and testing
- Use point-in-time recovery for critical data
- Implement proper backup retention and rotation policies
- Store backups in secure, off-site locations
- Implement proper disaster recovery procedures and testing
- Document recovery procedures and contact information

## Performance monitoring and tuning

- Monitor query execution times and identify slow queries
- Use appropriate connection pooling and resource management
- Implement proper caching strategies for frequently accessed data
- Monitor database statistics and performance metrics
- Use appropriate hardware sizing and resource allocation
- Implement proper partitioning strategies for large tables
- Use appropriate database configuration parameters
- Monitor and optimize memory and disk I/O usage

## Data migration and versioning

- Use proper migration scripts with version control
- Implement forward and backward migration capabilities
- Use proper testing and rollback procedures for migrations
- Document migration procedures and dependencies
- Implement proper data validation during migration
- Use appropriate downtime planning for major migrations
- Test migrations thoroughly in staging environments
- Implement proper migration logging and auditing

## Database-specific optimizations

- Use appropriate storage engines for different use cases
- Implement proper partitioning strategies for large tables
- Use appropriate clustering and replication for high availability
- Implement proper sharding strategies for horizontal scaling
- Use appropriate caching layers (application, database, query)
- Implement proper connection management and pooling
- Use appropriate database configuration parameters
- Monitor and optimize database-specific performance metrics

## Development and deployment practices

- Use version control for all database schema changes
- Implement proper environment-specific configurations
- Use proper database provisioning and automation
- Implement proper monitoring and alerting systems
- Use proper documentation and change management
- Implement proper testing strategies for database changes
- Use proper deployment procedures and rollback plans
- Implement proper capacity planning and scaling strategies

## Data governance and compliance

- Implement proper data classification and handling
- Use appropriate data retention policies
- Implement proper privacy and compliance controls
- Use proper audit trails and change tracking
- Implement proper data quality checks and validation
- Use appropriate data anonymization for non-production use
- Implement proper legal and regulatory compliance measures
- Document data handling procedures and policies
