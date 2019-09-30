### Initial thoughts

```sql
SELECT DISTINCT Salary AS SecondHighestSalary
FROM Employee
ORDER BY Salary DESC
LIMIT 1 OFFSET 1
```

The above solution will fail if there is no 2nd-highest salary.

### MySQL Solution

Since the 2nd-highest salary may not exist, use the [IFNULL()](https://www.w3schools.com/sql/func_mysql_ifnull.asp) function to account for `NULL`:

```sql
SELECT
  IFNULL(
    (SELECT DISTINCT Salary FROM Employee
     ORDER BY Salary DESC
     LIMIT 1 OFFSET 1),
    NULL)
AS SecondHighestSalary
```
