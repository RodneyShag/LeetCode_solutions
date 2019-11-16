### MySQL Solution

```sql
SELECT D.Name AS Department, E1.Name AS Employee, E1.Salary AS Salary
FROM Employee AS E1, Department AS D
WHERE E1.DepartmentId = D.Id AND
      (SELECT COUNT(DISTINCT E2.Salary)
      FROM Employee E2
      WHERE E1.DepartmentId = E2.DepartmentId AND
            E2.Salary > E1.Salary) < 3
```

### Notes

The subquery `SELECT COUNT...` counts how many Employees `E2` have a salary greater than Employee `E1`. That value must be less than 3 for the `E1` salary to be in the top 3 salaries.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/department-top-three-salaries/discuss/394442)
- [github.com/RodneyShag](https://github.com/RodneyShag)
