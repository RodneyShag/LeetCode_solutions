### Algorithm

- Use 2 pointers. let `i` point to 0th element in array, and `j` to point to last element in array.
- Sum the values at the 2 indexes.
    - If the sum is too small, increment `i` (so we can look at  larger values)
    - If the sum is too   big, decrement `j` (so we can look at smaller values)
    - If the sum equals `target`, we found a solution

### Example

```
target = 9

 i          j
[2  7  11  15]     2 + 15 = 17. Sum is bigger than 9. Decrement j.

 i      j
[2  7  11  15]     2 + 11 = 13. Sum is bigger than 9. Decrement j.

 i  j
[2  7  11  15]     2 + 7 = 9 = target. We found a solution.
```

### Solution

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        if (nums == null || nums.length < 2) {
            return null;
        }
        int i = 0;
        int j = nums.length - 1;
        while (i < j) {
            int sum = nums[i] + nums[j];
            if (sum < target) {
                i++;
            } else if (sum > target) {
                j--;
            } else {
                break;
            }
        }
        // Problem's output counts indexes starting at [1, 2...]
        return new int[]{i + 1, j + 1};
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/discuss/459056)
- [github.com/RodneyShag](https://github.com/RodneyShag)
