### MySQL Solution

```sql
SELECT     Request_at AS Day,
           ROUND(SUM(Status != "completed") / COUNT(*), 2) AS 'Cancellation Rate'
FROM       Trips AS t
INNER JOIN Users AS c ON t.Client_Id = c.Users_Id AND c.Banned = 'No'
INNER JOIN Users AS d ON t.Driver_Id = d.Users_Id AND d.Banned = 'No'
WHERE      Request_at BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY   Request_at;
```

### Alternate Solution

Instead of `INNER JOIN`, we can use separate `SELECT` queries:

```sql
SELECT   Request_at AS Day,
         ROUND(SUM(Status != "completed") / COUNT(*), 2) AS 'Cancellation Rate'
FROM     Trips
WHERE    (Request_at BETWEEN '2013-10-01' AND '2013-10-03') AND
         Client_Id IN (SELECT Users_Id FROM Users WHERE Banned = 'No') AND
         Driver_Id IN (SELECT Users_Id FROM Users WHERE Banned = 'No')
GROUP BY Request_at;
```
