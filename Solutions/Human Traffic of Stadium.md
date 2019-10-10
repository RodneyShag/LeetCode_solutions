### Algorithm

Use [SELF JOIN](https://www.w3schools.com/sql/sql_join_self.asp) to join the 3 stadium tables with themselves.

For entry `a`, we must account for 3 possible cases: Either `a` is 1st, 2nd, or 3rd in the 3 consecutive rows:

```
+---+      +---+      +---+
| a |      | b |      | c |
| b |      | a |      | b |
| c |      | c |      | a |
+---+      +---+      +---+
```

We don't need to account for the other 3 cases: [a c b], [c b a], [b c a] since those will give duplicate solutions for `a`.

### MySQL Solution

```sql
SELECT DISTINCT a.*
FROM stadium a, stadium b, stadium c
WHERE a.people >= 100 AND b.people >= 100 AND c.people >= 100
AND (
    (a.id + 1 = b.id AND a.id + 2 = c.id) OR -- a, b, c
    (b.id + 1 = a.id AND b.id + 2 = c.id) OR -- b, a, c
    (c.id + 1 = b.id AND c.id + 2 = a.id)    -- c, b, a
)
ORDER BY a.id
```

### Notes

Use the `DISTINCT` keyword to remove duplicates in our solution. If `a` fell in this spot:

```
+------+
|people|
+------+
|  200 |
|  200 |
|  200 | <-- a
|  200 |
|  200 |
+------+
```

we would have duplicates since `a` is the start of 3 consecutive rows, the middle of 3 consecutive rows, and the end of 3 consecutive rows.
