# Solution 1 - Binary Search

Use [binary search](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Binary%20Search.md) to keep guessing different `int` values that may qualify as the square root of `n`

### Code

```java
class Solution {
    public boolean isPerfectSquare(int n) {
        if (n < 0) {
            return false;
        }
        int lo = 0;
        int hi = n;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            long squared = (long) mid * mid; // use `long` to avoid integer overflow
            if (squared == n) {
                return true;
            } else if (squared < n) {
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        }
        return false;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(log n)
- Space Complexity: O(1)


# Solution 2 - Newton's Method

_Newton's Method_ is also an O(log n) solution, but is faster than binary search since it makes better guesses for the square root in each iteration of the `while` loop. [This LeetCode post](https://leetcode.com/problems/valid-perfect-square/discuss/130010/Python-4-Methods-with-time-testing) compares the actual runtimes of _binary search_ and _Newton's method_.

### Code

```java
class Solution {
    public boolean isPerfectSquare(int x) {
        if (x < 0) {
            return false;
        }
        long r = x; // use `long` so r*r is calculated as a `long`
        while (r*r > x) {
            r = (r + x/r) / 2;
        }
        return r*r == x;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(log n)
- Space Complexity: O(1)


# Links

- [Discuss on LeetCode](https://leetcode.com/problems/valid-perfect-square/discuss/459934)
- [github.com/RodneyShag](https://github.com/RodneyShag)
