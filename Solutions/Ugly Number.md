### Algorithm

Sample ugly numbers are 1, 2, 3, 4, 5, 6, 8, 9, 10, 12...

For a number to be an ugly number, it's prime factorization should only include 2, 3, and 5:

```
2
2 * 2
2 * 3
2 * 3 * 5
2 * 2 * 3 * 3 * 5 * 5 * 5
```

To find ugly numbers, we remove all factors of 2, 3, and 5 using division. If the end result is 1, then the original input was an ugly number.

### Solution

```java
class Solution {
    public boolean isUgly(int n) {
        if (n < 1) {
            return false;
        }
        int[] divisors = {2, 3, 5};
        for (int d : divisors) {
            while (n % d == 0) {
                n = n / d;
            }
        }
        return n == 1;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode]https://leetcode.com/problems/ugly-number/discuss/457835)
- [github.com/RodneyShag](https://github.com/RodneyShag)
