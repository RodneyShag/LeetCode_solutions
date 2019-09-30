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
