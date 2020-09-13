### Algorithm

This is a dynamic programming problem.

Let `dp[i]` represent the maximum amount of money you can rob from houses `0` to `i` inclusive.

```
dp[i] =

0                                          if i  < 0
nums[0]                                    if i == 0
Math.max(nums[0], nums[1])                 if i == 1
Math.max(dp[i - 1], dp[i - 2] + nums[i])   otherwise
```

which can be more concisely represented as:

```
dp[i] =

0                                          if i < 0
Math.max(dp[i - 1], dp[i - 2] + nums[i])   otherwise
```


### List of Solutions

| # |           Solutions            | Runtime |   Space   |  Preference  |
|:-:|:------------------------------:|:-------:|:---------:|:------------:|
| 1 | Dynamic Programming: Recursive |   O(n)  |   O(n)    |       -      |
| 2 | Dynamic Programming: Iterative |   O(n)  |   O(n)    |       -      |
| 3 | Iterative, no array            |   O(n)  |   O(1)    |   Favorite   |

### Solution 1 - Dynamic Programming: Recursive

```java
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int cache[] = new int[nums.length];
        Arrays.fill(cache, -1); // we fill -1 since a house can have 0 money.
        return rob(nums, cache, nums.length - 1);
    }

    private int rob(int[] nums, int[] cache, int n) {
        if (n < 0) { // this can happen due to our recursive calls
            return 0;
        } else if (cache[n] >= 0) {
            return cache[n];
        }
        cache[n] = Math.max(rob(nums, cache, n - 1), rob(nums, cache, n - 2) + nums[n]);
        return cache[n];
    }
}
```

### Solution 2 - Dynamic Programming: Iterative

```java
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        } else if (nums.length == 1) {
            return nums[0];
        }
        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        for (int i = 2; i < nums.length; i++) {
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
        }
        return dp[nums.length - 1];
    }
}
```

### Solution 3 - Iterative, no array

Notice that `dp[i]` only depends on `dp[i-1]` and `dp[i-2]`. So instead of storing all the results in the `dp` array, we can just save the previous 2 values.

```java
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        } else if (nums.length == 1) {
            return nums[0];
        } else if (nums.length == 2) { // new base case needed for 'no array' solution
            return Math.max(nums[0], nums[1]);
        }
        int prev2 = nums[0];
        int prev1 = Math.max(nums[0], nums[1]);
        int curr = 0;
        for (int i = 2; i < nums.length; i++) {
            curr = Math.max(prev1, prev2 + nums[i]);
            prev2 = prev1;
            prev1 = curr;
        }
        return curr;
    }
}
```

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
