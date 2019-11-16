### Algorithm

[Video explanation](https://www.youtube.com/watch?time_continue=350&v=jaNZ83Q3QGc)

### Solution

```java
class Solution {
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] += dp[i-coin];
            }
        }
        return dp[amount];
    }
}
```

### Notes

- In the general case, our solution may overflow our `int` return value. Can use a `long` instead.

### Time/Space Complexity

- Time Complexity: O(amount * coins)
- Space Complexity: O(amount)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/coin-change-2/discuss/304455)
- [github.com/RodneyShag](https://github.com/RodneyShag)
