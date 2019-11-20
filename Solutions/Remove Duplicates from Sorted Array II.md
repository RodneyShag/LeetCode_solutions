### Notes

- First solve [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array), then apply the same concepts here.
- Remember, the input array is _sorted_.

### Solution

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int i = 0;
        for (int n : nums) {
            if (i < 2 || nums[i - 2] != n) {
                nums[i] = n;
                i++;
            }
        }
        return i;
    }
}
```

### Implementation Notes

In the `for` loop, notice we only have to do the `nums[i - 2] != n` comparison.

A `nums[i - 1] != n` comparison is not necessary since the input array is sorted.


### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/discuss/433558)
- [github.com/RodneyShag](https://github.com/RodneyShag)
