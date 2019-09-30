### Notes

Use a [LEFT JOIN](https://www.w3schools.com/sql/sql_join_left.asp)

### MySQL Solution

```sql
SELECT Name AS Customers FROM Customers
LEFT JOIN Orders
ON Customers.Id = Orders.CustomerId
WHERE Orders.CustomerId IS NULL
```
