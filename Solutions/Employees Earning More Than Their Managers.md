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

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/employees-earning-more-than-their-managers/discuss/393527)
- [github.com/RodneyShag](https://github.com/RodneyShag)
