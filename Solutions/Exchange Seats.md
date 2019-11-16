### Algorithm

There are 3 cases
1. For students with even-numbered ids, subtract 1 from their id
1. For students with odd-numbered ids, add 1 to their id (Except if this odd-numbered student has the highest id in the class
1. For student with odd-numbered id who also has the highest id in the class, don't change the id.

### MySQL Solution

```sql
SELECT
    CASE
        WHEN id % 2 = 0 THEN id - 1
        WHEN id % 2 = 1 AND id != (SELECT COUNT(*) FROM seat) THEN id + 1
        ELSE id
    END as id,
    student
FROM seat
ORDER BY id
```

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/exchange-seats/discuss/393915)
- [github.com/RodneyShag](https://github.com/RodneyShag)
