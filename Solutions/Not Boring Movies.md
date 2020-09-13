### MySQL Solution

```sql
SELECT * FROM cinema
WHERE id % 2 = 1 AND
      description != 'boring'
ORDER BY rating DESC
```

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
