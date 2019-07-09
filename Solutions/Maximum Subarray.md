# Solution 1 - Dynamic Programming

### Clarifying Questions

You should ask the interviewer if
  1. negative numbers can exist in the array
  1. if subarrays of size 0 are allowed

If these are true, then we should never return a negative number. If our maximum sum is negative, just return 0 as our final answer.

### Algorithm

This is a dynamic programming problem.

Let `dp[i]` represent the maximum subarray that starts somewhere before `i`, and ends at `i`.

Base case:
```
dp[0] = A[0]
```
Recursive case:
```
dp[i] = Math.max(dp[i - 1] + A[i], A[i])
```

### Example

```
input array: [1, 0, -5, 3]
```
Following our algorithm, we will get:

```
dp array: [1, 1, -4, 3]
```
and our solution will be the largest value in the `dp` array

### Code

```java
class Solution {
    public int maxSubArray(int[] A) {
        if (A == null || A.length == 0) {
            throw new IllegalArgumentException();
        }
        int[] dp = new int[A.length];
        dp[0] = A[0];
        int maxSum = A[0];
        for (int i = 1; i < A.length; i++) {
            dp[i] = Math.max(dp[i - 1] + A[i], A[i]);
            maxSum = Math.max(maxSum, dp[i]);
        }
        return maxSum;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

# Solution 2 - Optimizing Space Complexity

### Algorithm

Notice that `dp[i]` only depends on `dp[i-1]`. So instead of storing all the results in the `dp` array, we can just save the previous value.

### Code

```java
class Solution {
    public int maxSubArray(int[] A) {
        if (A == null || A.length == 0) {
            throw new IllegalArgumentException();
        }
        int maxEndingHere = A[0];
        int maxSum = A[0];
        for (int i = 1; i < A.length; i++) {
            maxEndingHere = Math.max(maxEndingHere + A[i], A[i]);
            maxSum = Math.max(maxSum, maxEndingHere);
        }
        return maxSum;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)
