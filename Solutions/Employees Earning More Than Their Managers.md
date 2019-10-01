### Hint

Use a [SELF JOIN](https://www.w3schools.com/sql/sql_join_self.asp)

### MySQL Solution

```sql
SELECT
    a.Name AS Employee
FROM
    Employee AS a,
    Employee AS b
WHERE
    a.ManagerId = b.Id AND a.Salary > b.Salary
```
