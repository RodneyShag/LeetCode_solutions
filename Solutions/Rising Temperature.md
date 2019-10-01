### Hint

- Use a [SELF JOIN](https://www.w3schools.com/sql/sql_join_self.asp)
- Use the built-in [DATEDIFF](https://dev.mysql.com/doc/refman/5.7/en/date-and-time-functions.html#function_datediff) function to find the number of days that 2 `Date`s differ by.

### MySQL Solution

```sql
SELECT w1.Id
FROM
  Weather as w1,
  Weather as w2
WHERE
  DATEDIFF(w1.RecordDate, w2.RecordDate) = 1 AND
  w1.Temperature > w2.Temperature
```
