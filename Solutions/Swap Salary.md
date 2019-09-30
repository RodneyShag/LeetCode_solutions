### MySQL Solution

```sql
UPDATE salary
SET sex = IF(sex = 'm', 'f', 'm');
```
