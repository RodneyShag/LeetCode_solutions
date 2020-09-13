# Solution 1

### Algorithm

This is a dynamic programming problem.

- Let `buy[i]` be max profit until index `i` in `[0, i]` where we did a buy and still own the stock.
- Let `sell[i]` be max profit until index `i` in `[0, i]` where we don't own any stock.

### Code

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length <= 1) {
            return 0;
        }
        int[] buy = new int[prices.length];
        int[] sell = new int[prices.length];

        // Base cases
        buy[0] = -prices[0];                          // buy on 0th day
        buy[1] = Math.max(-prices[0], -prices[1]);    // buy whichever day is cheaper
        sell[0] = 0;                                  // can't sell yet
        sell[1] = Math.max(0, prices[1] - prices[0]); // buy day 0 sell day 1, if profitable

        for (int i = 2; i < prices.length; i++) {
            buy[i] = Math.max(
                buy[i - 1],             // do nothing today
                sell[i - 2] - prices[i] // sell 2+ days ago, buy today
            );
            sell[i] = Math.max(
                sell[i - 1],           // do nothing today
                buy[i - 1] + prices[i] // buy 1+ days ago, sell today
            );
        }
        return sell[prices.length - 1];
    }
}
```


### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)


# Solution 2

### Optimizing Space Complexity

Since we only need to access the previous 2 elements in our arrays, we can save just the previous 2 elements in each array instead of saving the each entire array.

- Let `b2`, `b1`, `b0` represent `buy[i - 2]`, `buy[i - 1]`, `buy[i]`
- Let `s2`, `s1`, `s0` represent `sell[i - 2]`, `sell[i - 1]`, `sell[i]`
- Our loop will start from `i = 2`, so initially:
    - `b2` and `s2` will represent 0th element
    - `b1` and `s1` will represent 1th element
    - `b0` and `s0` will represent 2th element

```java
[_,  _,  _,  _,  _]
 b2  b1  b0
 s2  s1  s0
```

Since we actually won't be using `b2` to calculate a solution, we can omit it in the code below.

### Code

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length <= 1) {
            return 0;
        } else if (prices.length == 2) {
            return Math.max(0, prices[1] - prices[0]);
        }
        int b1 = Math.max(-prices[0], -prices[1]);
        int b0 = 0;
        int s2 = 0;
        int s1 = Math.max(0, prices[1] - prices[0]);
        int s0 = 0;
        for (int i = 2; i < prices.length; i++) {
            b0 = Math.max(b1, s2 - prices[i]);
            s0 = Math.max(s1, b1 + prices[i]);
            b1 = b0;
            s2 = s1;
            s1 = s0;
        }
        return s0;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

# Alternate solutions

A [1-array solution](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/discuss/240097) and [3-array solution](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/discuss/293789) also exist, but I still prefer my solutions above.

# Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
