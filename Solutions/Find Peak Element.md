### Notes

- We are given `nums[-1] = nums[n] = negative infinity`. This ensures we have at least 1 local maximum.
- A simple O(n) solution exists by checking each element linearly, but let's try to solve it in O(log n) instead.

### Algorithm

- The key insight is that we only need to find 1 peak element. _Any_ peak element will do.
- By doing binary search and comparing `A[mid]` to `A[mid + 1]`, we can see which side has a guaranteed peak maximum and recurse on just that side.

### Solution

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int start = 0;
        int end = nums.length - 1;
        while (start < end) {
            int mid = (start + end) / 2;
            if (nums[mid] > nums[mid + 1]) {
                end = mid;
            } else {
                start = mid + 1;
            }
        }
        return start;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(log n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/find-peak-element/discuss/304478)
- [github.com/RodneyShag](https://github.com/RodneyShag)
