### Hints

Use [GROUP BY](https://www.w3schools.com/sql/sql_groupby.asp) on `id`, so that the different `month` values for the same `id` can be combined.

### MySQL Solution

```sql
SELECT
    id,
    MAX(IF(month = 'Jan', revenue, null)) AS Jan_Revenue,
    MAX(IF(month = 'Feb', revenue, null)) AS Feb_Revenue,
    MAX(IF(month = 'Mar', revenue, null)) AS Mar_Revenue,
    MAX(IF(month = 'Apr', revenue, null)) AS Apr_Revenue,
    MAX(IF(month = 'May', revenue, null)) AS May_Revenue,
    MAX(IF(month = 'Jun', revenue, null)) AS Jun_Revenue,
    MAX(IF(month = 'Jul', revenue, null)) AS Jul_Revenue,
    MAX(IF(month = 'Aug', revenue, null)) AS Aug_Revenue,
    MAX(IF(month = 'Sep', revenue, null)) AS Sep_Revenue,
    MAX(IF(month = 'Oct', revenue, null)) AS Oct_Revenue,
    MAX(IF(month = 'Nov', revenue, null)) AS Nov_Revenue,
    MAX(IF(month = 'Dec', revenue, null)) AS Dec_Revenue
FROM Department
GROUP BY id
```

### MAX vs SUM

It seems the test data does not have duplicate data, so you can either use `MAX` or `SUM` and the solution will work.

For a specific `id`, since the input data does not have duplicates, we only have 1 `Jan`, 1 `Feb`, 1 `Mar`, etc., so whether we use `MAX` or `SUM`, the column will just display that `revenue`.

The `MAX` lets us combine each `revenue` with `null` and selects that 1 `revenue` for the cell.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/reformat-department-table/discuss/393818)
- [github.com/RodneyShag](https://github.com/RodneyShag)
