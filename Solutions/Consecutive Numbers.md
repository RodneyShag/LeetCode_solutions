### Notes

We assume the `Id` column increases sequentially by 1 for every row. Otherwise, the below solution would not work properly.

The below solution uses a [SELF JOIN](https://www.w3schools.com/sql/sql_join_self.asp).

### MySQL Solution

```sql
SELECT DISTINCT l1.Num AS ConsecutiveNums
FROM
    Logs AS l1,
    Logs AS l2,
    Logs AS l3
WHERE
    l1.Id + 1 = l2.Id AND
    l2.Id + 1 = l3.Id AND
    l1.Num = l2.Num AND
    l2.Num = l3.Num
```

### Why use `Distinct`?

Without `Distinct`, this test case fails:

```
Input: {"headers": {"Logs": ["Id", "Num"]}, "rows": {"Logs": [[1, 3], [2, 3], [3, 3], [4, 3]]}}
Output: {"headers": ["ConsecutiveNums"], "values": [[3], [3]]}
Expected: {"headers":["ConsecutiveNums"],"values":[[3]]}
```

since for `[3,3]`, it's a match for `[1,3], [2,3], [3,3]` and also for `[2,3], [3,3], [4,3]`.  We end up matching on `[3,3]` twice, and the `l1.Num` on it incorrectly gives us `[3]` twice

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
