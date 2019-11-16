### MySQL Solution

```sql
SELECT * FROM cinema
WHERE id % 2 = 1 AND
      description != 'boring'
ORDER BY rating DESC
```

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/not-boring-movies/discuss/393788)
- [github.com/RodneyShag](https://github.com/RodneyShag)
