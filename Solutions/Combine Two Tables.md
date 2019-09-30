### MySQL Solution

```sql
SELECT FirstName, LastName, City, State FROM Person
LEFT JOIN Address USING(PersonId)
```

### Notes

We could also replace

```sql
USING(PersonId)
```

with

```sql
ON Person.PersonId = Address.PersonId
```

The `ON` clause is used to join tables where the column names don’t match in both tables.
