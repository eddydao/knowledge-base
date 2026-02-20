# Workflow of a SQL query (SQL server)
1. User authenticates to SQL server in a client application and submits a query
2. SQL Server parses the query and checks for any syntax errors
3. Resolves all objects, tables and columns in the query, performs check on column data types in Algebrizer. Algebrizer generates a query process tree and a query hash. If the execution plan already exists, SQL server uses that cached plan and executes the query
4. If no query plan exists, the Query Optimizer performs a full cost-based optimization with the help of statistics, query process tree and constraints => prepares the cost-optimized SQL server execution plan
5. Execute the SQL according to the plan and returns the results.

> Sql server provides estimated and actual execution plans, which may be differ.

# Why estimated and actual plan differ

## Stale statistics
- Primary reason
- Happen when statistics are not updated, or data sampling is not appropriate
- The query optimizer will perform a full optimization and build a execution plan based on old information
> Occur when data changes frequently and statistics are not updated according to index maintenance.

## Serial or parallel SQL execution plan
- The query optimized produces a serial or parallel plan depending upon query cost and cost threshold of parallelism 
=> SQL may choose diff plan

## Invalid estimates
- Some objects will be created at runtime, then the estimated plan will not accurate due to error in compile time

# Using the execution plan
- Each step in the execution plan is called node/operator:
	- Seq scan
	- Index scan
	- Join ops
	- Aggregate
	- Sort
- Cost estimated: 
- Row
- Actual time
- Loop: 