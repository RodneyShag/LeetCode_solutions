### Algorithm

We can use a modified version of [binary search](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Binary%20Search.md).

Since it is possible that we want to insert at the end of the array, instead of searching from `0` to `nums.length - 1`, we will search from `0` to `nums.length`.

### Solution

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        if (nums == null) {
            return 0;
        }
        int lo = 0;
        int hi = nums.length;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] < target) {
                lo = mid + 1;
            } else {
                hi = mid;
            }
        }
        return lo;
    }
}
```

### Implementation Details

Instead of calculating the middle value as `mid = (lo + hi) / 2`, do `mid = lo + (hi - lo) / 2` to avoid integer overflow.

### Time/Space Complexity

-  Time Complexity: O(log n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
