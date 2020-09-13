### Hint

Use a [SELF JOIN](https://www.w3schools.com/sql/sql_join_self.asp)

### MySQL Solution

```sql
DELETE p1
FROM
    Person AS p1,
    Person AS p2
WHERE
    p1.Email = p2.Email AND
    p1.Id > p2.Id
```

### Example

Input:

```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
```

The table after the implicit join and the `WHERE p1.Email = p2.Email`:

```
+-------+------------------+-------+------------------+
| p1.Id | p1.Email         | p2.Id | p2.Email
+-------+------------------+-------+------------------+
|   1   | john@example.com |   1   | john@example.com |
|   3   | john@example.com |   1   | john@example.com |
|   2   | bob@example.com  |   1   | bob@example.com  |
|   1   | john@example.com |   3   | john@example.com |
|   3   | john@example.com |   3   | john@example.com |
+-------+------------------+-------+------------------+
```
The following row matches the criteria of `p1.Id > p2.Id`:

```
|   3   | john@example.com |   1   | john@example.com |
```

In our original `p1` table this row will be deleted:

```
| 3  | john@example.com |
```

Now `p1` is our final table:

```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
```

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
