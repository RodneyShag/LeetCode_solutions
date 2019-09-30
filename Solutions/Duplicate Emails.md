### Notes

Use the [HAVING](https://www.w3schools.com/sql/sql_having.asp) clause since the `WHERE` clause doesn't support aggregate functions

### MySQL Solution

```sql
SELECT Email FROM Person
GROUP BY Email
HAVING Count(Email) > 1
```
