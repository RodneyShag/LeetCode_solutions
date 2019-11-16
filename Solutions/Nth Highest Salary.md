### MySQL Solution

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  DECLARE M INT;
  SET M = N - 1;
  RETURN (
    SELECT DISTINCT Salary FROM Employee
    ORDER BY Salary DESC
    LIMIT 1 OFFSET M
  );
END
```

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/nth-highest-salary/discuss/393481)
- [github.com/RodneyShag](https://github.com/RodneyShag)
