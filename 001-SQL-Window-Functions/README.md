# Day 001 - SQL Window Functions

## What I Learned

Today I learned how SQL Window Functions allow calculations across rows while retaining row-level detail.

## Why This Matters
 
Traditional aggregate functions such as SUM() and COUNT() can collapse rows when used with GROUP BY.
 
Window Functions allow calculations across a set of rows while preserving the individual rows in the result set.
 
This makes them useful for ranking, running totals, moving averages, and comparisons within groups of data.

## Example: ROW_NUMBER()
 
Suppose we have a table of employees and their salaries.
 
```sql
SELECT
EmployeeID,
EmployeeName,
Salary,
ROW_NUMBER() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;
```
 
### What This Does
 
The ROW_NUMBER() function assigns a unique number to each row based on the order specified.
 
In this example, employees are ranked from the highest salary to the lowest salary.

## ROW_NUMBER() vs RANK() vs DENSE_RANK()
 
Consider the following salaries:
 
| Employee | Salary |
|----------|---------|
| Alice | 10000 |
| Bob | 9000 |
| Charlie | 9000 |
| David | 8000 |
 
### Using RANK()
 
```sql
SELECT
EmployeeName,
Salary,
RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;
```
 
Result:
 
- Alice = 1
- Bob = 2
- Charlie = 2
- David = 4
 
Notice that rank 3 is skipped.

### Using DENSE_RANK()

```sql
SELECT
    EmployeeID,
    EmployeeName,
    Salary,
    DENSE_RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;
```

Sample Data:

| EmployeeID | EmployeeName | Salary |
|------------|--------------|---------|
| 1 | Alice | 10000 |
| 2 | Bob | 9000 |
| 3 | Charlie | 9000 |
| 4 | David | 8000 |

Result:

| EmployeeID | EmployeeName | Salary | SalaryRank |
|------------|--------------|---------|------------|
| 1 | Alice | 10000 | 1 |
| 2 | Bob | 9000 | 2 |
| 3 | Charlie | 9000 | 2 |
| 4 | David | 8000 | 3 |

### Observation

DENSE_RANK() assigns the same rank to rows with equal values.

Unlike RANK(), it does not leave gaps in the ranking sequence. Since Bob and Charlie share rank 2, the next rank assigned is 3 rather than 4.

## Key Takeaways

- Window Functions perform calculations across rows without collapsing the result set.
- ROW_NUMBER() assigns a unique number to every row.
- RANK() assigns the same rank to tied values and skips subsequent ranks.
- DENSE_RANK() assigns the same rank to tied values without skipping ranks.
- Window Functions are commonly used for ranking, running totals, trend analysis, and analytical reporting.
