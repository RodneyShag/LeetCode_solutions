### Algorithm

1. Count the number of occurrences of each number in the array. Save these counts in a `Map`.
1. Check if any of the "values" in the `Map` are repeated:
    - put all the `Map` values in a `Set`
    - compare the sizes of the `Map` and `Set`. If they're the same size, then the `Map` has all unique values.

### Solution

```java
class Solution {
    public boolean uniqueOccurrences(int[] nums) {
        if (nums == null) {
            return true;
        }

        Map<Integer, Integer> map =  new HashMap();
        for (int n : nums) {
            map.merge(n, 1, Integer::sum);
        }

        Set<Integer> set = new HashSet(map.values());
        return map.size() == set.size();
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
