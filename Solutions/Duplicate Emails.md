### Hints

Use [GROUP BY](https://www.w3schools.com/sql/sql_groupby.asp) on `Email` to see how many of each `Id` there exists for each email.

Use the [HAVING](https://www.w3schools.com/sql/sql_having.asp) clause since the `WHERE` clause doesn't support aggregate functions

### MySQL Solution

```sql
SELECT Email FROM Person
GROUP BY Email
HAVING Count(Email) > 1
```

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
