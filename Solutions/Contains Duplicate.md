### Hint

Use a `HashSet` to detect duplicates.

### Solution

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet();
        for (int num : nums) {
            if (set.contains(num)) {
                return true;
            }
            set.add(num);
        }
        return false;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/contains-duplicate/discuss/432778)
- [github.com/RodneyShag](https://github.com/RodneyShag)
