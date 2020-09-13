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

- It seems the input data has at most 1 row for every `id` and `month` pair, so the revenue for an `id` and `month` pair will always be a single value
- Therefore, for a specific `id`, we can only have 1 value for each of `Jan`, `Feb`, `Mar`, etc.
- Since multiple rows in the input can have the same `id`, the `GROUP BY` needs an aggregate function (such as `MAX` or `SUM`) to combine the rows for an `id`. Since each `id` and `month` pair can only have 1 `revenue`, it doesn't matter whether we use `MAX` or `SUM` for combining rows
- I use `MAX`. If the `month` has a revenue, it will use it, otherwise, the value will be `null`

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
