### MySQL Solution

```sql
SELECT D.Name AS Department, E.Name AS Employee, E.Salary AS Salary
FROM Employee AS E, Department AS D
WHERE E.DepartmentId = D.Id AND
      E.Salary = (SELECT MAX(Salary) FROM Employee WHERE Employee.DepartmentId = D.Id)
```

### Notes

The part after the `AND` finds the `MAX` salary for the `Department` we're interested in.

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
