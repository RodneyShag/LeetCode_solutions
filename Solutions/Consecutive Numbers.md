### Notes

We assume the `Id` column increases sequentially by 1 for every every row. Otherwise, the below solution would not work properly.

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
