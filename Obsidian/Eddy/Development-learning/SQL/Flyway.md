SQL versioning for Java sql databases

The fundamental unit of Flyway is called a migration: a collection of SQL statements that run together.
Each migration has its own SQL file.

Naming convention ( mostly):
`Prefix_version_separator_description`
- Prefix: single letter describing the migrating type (**V**ersion, **U**ndo, **R**epeat)
- Version: number punctuated by underscore instead of period ( 1, 1_1, 1_2,...) 
- Separator: 2 underscore (__)
- description: what the migration does, in snake case

**Undo migrations**: optional migrations that Flyway can use to roll back and recover from any version that fail.

**Repeat migrations**: executed every time Flyway runs regardless of the current database version.

## Database version
Flyway checks the current version of database when migrates
-> only applying the migration scripts that have a higher version number
> Current version number saved in `flyway_schema_history` table in database

## Configuration
1. Add dependency
2. Setup in `application.yml`
```yaml
spring: 
	flyway:
		url:'jdbc:...'
		schemas: 'my_schema'
		user: 'my-database-user'
		password: 'my-password'
		locations: classpath:db/migration
```

The `location` property specifying the location that has migrations, common choice is to tell Flyway to scan Java classpath

`locations: filesystem:sql/migration`: this will tell Flyway to scan directory outside the Java classpath

## Tips
### **Always set `cleanDisabled` to true in production env**: 
Make sure Flyway doesn't drop the data when accidentally change migration commit history

### **Always write idempotent migrations**: 
- Use `If` statement to make the migration idempotent
- Some database platform don't allow `IF ELSE` logic, the common practice is to wrap each migration's logic in its own stored procedure. Basic pattern: 
	- Drop procedure if exist
	- create new procedure `this_migration_name` that defines as...
	- If database in state A, execute the migration logic to bring to state B
	- call the new procedure `this_migration_name`
	- drop procedure `this_migration_name` if exist
### Consider splitting up large migrations
Important if need to define **Undo** migrations.
If the database doesn't allow DDL transactions and need to manually define rollback plans, keeping the versioned migrations as small and concise as possible.

### For big project, consider using timestamp versions

