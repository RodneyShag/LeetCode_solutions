# Solution with Division

1. Multiply all the numbers together to get a product.
1. For each `i` in `int[] nums`, take the above product and divide it by `nums[i]`

The following 2 edge cases give us a product of 0, so they should be dealt with separately:

1. Input array with one 0 in it.
1. Input array with two or more 0s in it.

There are 2 reasons not to use this solution:

1. The product may cause integer overflow.
1. This LeetCode problem doesn't allow using division.

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)


# Solution without Division

At each index `i` in our result array, its value should be: `(product of all numbers to the left of nums[i]) * (product of all numbers to the right of nums[i])`

### Algorithm

Create 3 arrays with same length as the input array.

1. `int[] L` will have `L[i]` be the product of `L[0]` to `L[i-1]` inclusive.
    - Base case is `L[0] = 1`.
1. `int[] R` will have `R[i]` be the product of `R[i + 1]` to `R[R.length - 1]` inclusive.
    - Base case is `R[R.length - 1] = 1`
1. `int[] result` can be calculated using `result[i] = L[i] * R[i]`

### Solution

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        if (nums == null || nums.length <= 1) { // bad input
            return null;
        }
        int[] L = new int[nums.length];
        int[] R = new int[nums.length];

        L[0] = 1;
        for (int i = 1; i < L.length; i++) {
            L[i] = L[i - 1] * nums[i - 1];
        }

        R[R.length - 1] = 1;
        for (int i = R.length - 2; i >= 0; i--) {
            R[i] = R[i + 1] * nums[i + 1];
        }

        int[] result = new int[nums.length];
        for (int i = 0; i < result.length; i++) {
            result[i] = L[i] * R[i];
        }
        return result;
    }
}
```

### Example

```
  nums: [ 1,  2,  3,  4]
     L: [ 1,  1,  2,  6]
     R: [24, 12,  4,  1]
result: [24, 12,  8,  6]
```

Still confused? Check out [LeetCode's Solution 1](https://leetcode.com/problems/product-of-array-except-self/solution), which is the same as my solution and has an excellent detailed explanation.

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

LeetCode's follow-up question to "solve it with constant space complexity" can be ignored since the output array takes up O(n) space. The output array should not be omitted from the space complexity analysis.


# Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
