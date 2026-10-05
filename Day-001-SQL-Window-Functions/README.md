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

