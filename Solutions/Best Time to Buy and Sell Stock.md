### Algorithm

1. Iterate through the array. While iterating, keep track of 2 variables
    - `min` representing the minimum value you've seen so far
    - `maxProf` representing the maximum profit that can be generated (through a buy/sell) so far.
1. Return `maxProf`

### Solution

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }
        int min = prices[0];
        int maxProf = 0;
        for (int price : prices) {
            min = Math.min(min, price);
            maxProf = Math.max(maxProf, price - min);
        }
        return maxProf;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Variation of problem

[This post](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/discuss/39038) inspired a variation of the problem below.

Instead of giving stock prices `{1, 7, 4, 11}`, the interviewer may give the differences of prices between successive days `{0, 6, -3, 7}`.

In this case, we need to find a contiguous subarray giving the maximum profit. If the profit falls below 0, reset it to 0.

```java
public int maxProfit(int[] prices) {
    int maxCur = 0
    int maxSoFar = 0;
    for(int i = 1; i < prices.length; i++) {
        maxCur = Math.max(0, maxCur + prices[i] - prices[i - 1]);
        maxSoFar = Math.max(maxSoFar, maxCur);
    }
    return maxSoFar;
}
```

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
