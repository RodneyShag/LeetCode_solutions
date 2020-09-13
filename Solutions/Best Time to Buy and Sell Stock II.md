### Algorithm

Here's a sample graph of Price/Day:

```
P  \        /\  /\
R   \  /\  /  \/  \
I    \/  \/        \  /
C                   \/
E                   
            Day
```

We can always buy at the stock prices "local min" and sell at the stock prices "local max". So all we need to keep track of is how much the price increased between every pair of [local min, local max].

To calculate our total profit, every time the stock price increases, we add the price increase to our total profit.

### Solution

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null) {
            return 0;
        }
        int profit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1])
                profit += prices[i] - prices[i - 1];
        }
        return profit;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
