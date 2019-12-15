### Algorithm

Starting from the right of the number, look at each digit to see if it's a 1. Use an __unsigned__ bit shift as `n = n >>> 1` to shift the digits to the right by 1.

### Solution

```java
public class Solution {
    public int hammingWeight(int n) {
        int bits = 0;
        while (n != 0) {
            if ((n & 1) == 1) {
                bits++;
            }
            n = n >>> 1;
        }
        return bits;
    }
}
```

### Implementation Details

- Use `while (n != 0)` instead of `while (n > 0)` since `n` can be a negative number
- Put parentheses around `n & 1` as `((n & 1) == 1)` so that the `n & 1` is evaluated first

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/number-of-1-bits/discuss/451746)
- [github.com/RodneyShag](https://github.com/RodneyShag)
