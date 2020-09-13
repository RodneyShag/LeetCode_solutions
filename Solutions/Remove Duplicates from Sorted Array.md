### Notes

Remember, the input array is _sorted_.

### Solution

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int i = 0;
        for (int n : nums) {
            if (i == 0 || nums[i - 1] != n) {
                nums[i] = n;
                i++;
            }
        }
        return i;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Similar Problems

[Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
