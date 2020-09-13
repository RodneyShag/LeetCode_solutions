### Initial thoughts

```sql
SELECT DISTINCT Salary AS SecondHighestSalary
FROM Employee
ORDER BY Salary DESC
LIMIT 1 OFFSET 1
```

The above solution will fail if there is no 2nd-highest salary.

### MySQL Solution

Since the 2nd-highest salary may not exist, we have to turn our original query into a subquery, and wrap it in a `Select`:

```sql
SELECT
  (
    SELECT DISTINCT Salary FROM Employee
    ORDER BY Salary DESC
    LIMIT 1 OFFSET 1
  )
AS SecondHighestSalary
```

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
