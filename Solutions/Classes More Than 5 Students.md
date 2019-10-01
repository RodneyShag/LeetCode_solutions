### Hints

Use [GROUP BY](https://www.w3schools.com/sql/sql_groupby.asp) on `class` and find the [COUNT](https://www.w3schools.com/sql/sql_count_avg_sum.asp) of students in each `class`.

Use the [HAVING](https://www.w3schools.com/sql/sql_having.asp) clause since the `WHERE` clause doesn't support aggregate functions

### Notes

If the table was designed properly without duplicate entries, the following code would work:

```sql
SELECT class FROM courses
GROUP BY class
HAVING COUNT(class) >= 5
```

However, the duplicate entries in the table prevent the above code from working properly.

### MySQL Solution

We use `DISTINCT` to remove the duplicate entries.

```sql
SELECT class FROM courses
GROUP BY class
HAVING COUNT(DISTINCT student) >= 5
```
