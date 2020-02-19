### Algorithm

1. Create a class variable called `int[] sum`.
1. Let `sum[i]` represent the sum from `num[0]` to `num[i]` inclusive.
1. To calculate `sumRange(int i, int j)`, just return `sum[j] - sum[i - 1]`
    - if `i == 0`, treat that as a special case

### Solution

```java
class NumArray {
    private int[] sum;

    public NumArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }
        sum = new int[nums.length];
        sum[0] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            sum[i] = sum[i - 1] + nums[i];
        }
    }

    public int sumRange(int i, int j) { // assumes 0 <= i <= j, and 'int[] sum' is not empty
        if (i == 0) {
            return sum[j];
        } else {
            return sum[j] - sum[i - 1];
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) to pre-compute. O(1) for `sumRange()` calls after precomputation.
- Space Complexity: O(n)

### Links

- [Discuss on LeetCode]https://leetcode.com/problems/range-sum-query-immutable/discuss/489951)
- [github.com/RodneyShag](https://github.com/RodneyShag)
