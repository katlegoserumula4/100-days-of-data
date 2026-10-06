002 - Common Table Expressions (CTEs)

WITH clause defines a CTE

A Common Table Expression (CTE) is a temporary named result set that exists only for the duration of a query.

CTEs improve readability by breaking complex queries into smaller logical steps.

They are used for transformations, aggregations, ranking, and building layered business logic.

## Syntax

```sql
WITH CTE_Name AS
(
    SELECT column1,
           column2
    FROM table_name
)
SELECT *
FROM CTE_Name;
| Employee | SalesAmount |
| -------- | ----------: |
| Alice    |       12000 |
| Bob      |        9000 |
| Charlie  |       15000 |
| David    |        8000 |
| Emma     |       11000 |


WITH HighPerformers AS
(
    SELECT
        Employee,
        SalesAmount
    FROM Sales
    WHERE SalesAmount > 10000
)
SELECT *
FROM HighPerformers;


## Real-World Application

As SQL queries become more complex, CTEs help divide business logic into smaller and easier-to-understand sections.

Instead of writing one large query, a developer can create multiple CTEs that each perform a specific task before combining them into a final result.
