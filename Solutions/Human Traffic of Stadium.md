### Algorithm

Use [SELF JOIN](https://www.w3schools.com/sql/sql_join_self.asp) to join the 3 stadium tables with themselves.

For entry `a`, we must account for 3 possible cases: Either `a` is 1st, 2nd, or 3rd in the 3 consecutive rows:

```
+---+      +---+      +---+
| a |      | _ |      | _ |
| _ |      | a |      | _ |
| _ |      | _ |      | a |
+---+      +---+      +---+
```

### MySQL Solution

```sql
SELECT DISTINCT a.*
FROM stadium a, stadium b, stadium c
WHERE a.people >= 100 AND b.people >= 100 AND c.people >= 100
AND (
    (a.id + 1 = b.id AND a.id + 2 = c.id) OR -- a is 1st in 3 consecutive rows
    (a.id - 1 = b.id AND a.id + 1 = c.id) OR -- a is 2nd in 3 consecutive rows
    (a.id - 2 = b.id AND a.id - 1 = c.id)    -- a is 3rd in 3 consecutive rows
)
ORDER BY a.id
```

### Example

We start with:
```
+------+------------+-----------+
| id   | visit_date | people    |
+------+------------+-----------+
| 1    | 2017-01-01 | 10        |
| 2    | 2017-01-02 | 109       |
| 3    | 2017-01-03 | 150       |
| 4    | 2017-01-04 | 99        |
| 5    | 2017-01-05 | 145       |
| 6    | 2017-01-06 | 1455      |
| 7    | 2017-01-07 | 199       |
| 8    | 2017-01-08 | 188       |
+------+------------+-----------+
```

The `WHERE` clause (in solution above) only keeps rows with more than 100 people. We then have 3 identical tables to join together:

```
          Table a                             Table b                             Table c
+------+------------+-----------+   +------+------------+-----------+   +------+------------+-----------+
| id   | visit_date | people    |   | id   | visit_date | people    |   | id   | visit_date | people    |
+------+------------+-----------+   +------+------------+-----------+   +------+------------+-----------+
| 2    | 2017-01-02 | 109       |   | 2    | 2017-01-02 | 109       |   | 2    | 2017-01-02 | 109       |
| 3    | 2017-01-03 | 150       |   | 3    | 2017-01-03 | 150       |   | 3    | 2017-01-03 | 150       |
| 5    | 2017-01-05 | 145       |   | 5    | 2017-01-05 | 145       |   | 5    | 2017-01-05 | 145       |
| 6    | 2017-01-06 | 1455      |   | 6    | 2017-01-06 | 1455      |   | 6    | 2017-01-06 | 1455      |
| 7    | 2017-01-07 | 199       |   | 7    | 2017-01-07 | 199       |   | 7    | 2017-01-07 | 199       |
| 8    | 2017-01-08 | 188       |   | 8    | 2017-01-08 | 188       |   | 8    | 2017-01-08 | 188       |
+------+------------+-----------+   +------+------------+-----------+   +------+------------+-----------+
```

The `AND` clause (in solution above) has the following matches:
- For `a.id = 2`, we have no match
- For `a.id = 3`, we have no match
- For `a.id = 5`, we have a match for `a.id = 5`, `b.id = 6`, `c.id = 7`
- For `a.id = 6`, we have a match for:
  - `a.id = 6`, `b.id = 7`, `c.id = 8`
  - `a.id = 6`, `b.id = 5`, `c.id = 7`
- For `a.id = 7`, we have a match for:
  - `a.id = 7`, `b.id = 6`, `c.id = 8`
  - `a.id = 7`, `b.id = 5`, `c.id = 6`
- For `a.id = 8`, we have a match for `a.id = 8`, `b.id = 6`, `c.id = 7`

We have successfully matched `a.id` of `5`, `6`, `7`, `8`, however, we have duplicate matches for ids `6` and `7`. We use `DISTINCT` in `SELECT DISTINCT a.*` to remove the duplicate matches.

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
