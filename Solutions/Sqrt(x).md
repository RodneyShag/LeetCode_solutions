# Solution 1 - Binary Search

### Assumptions

We assume input `x` is non-negative (0 or more) as stated in the problem.

### Algorithm

- If we find a number `m` where m<sup>2</sup> <= x and (m + 1)<sup>2</sup> > x, then `m` is `sqrt(x)` due to truncation. Example:
    - If `x` is 10, and `m` is 3, then we have
        - m<sup>2</sup> = 9 which is less than x
        - (m + 1)<sup>2</sup> = 16 which is greater than `x`
    - So sqrt(10) = 3 due to truncation of decimal digits.

Use [binary search](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Binary%20Search.md) to find `m`

### Solution

```java
class Solution {
    public int mySqrt(int x) {
        if (x == 0) {
            return 0;
        }
        int lo = 1;
        int hi = x;
        while (true) {
            int mid = lo + (hi - lo) / 2;
            if (mid <= x / mid && (mid + 1) > x / (mid + 1)) {
                return mid;
            } else if (mid < x / mid) {
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        }
    }
}
```

### Avoiding integer overflow

- We rewrote `mid = (lo + hi) / 2` as  `mid = lo + (hi - lo) / 2` to avoid integer overflow
- We rewrote `mid * mid <= x` as `mid <= x / mid` to avoid integer overflow

### Time/Space Complexity

-  Time Complexity: O(log n)
- Space Complexity: O(1)


# Solution 2 - Newton's Method

_Newton's Method_ is also an O(log n) solution, but is faster than binary search since it makes better guesses for the square root in each iteration of the `while` loop.

### Code

```java
class Solution {
    public int mySqrt(int x) {
        if (x == 0) {
            return 0;
        }
        long r = x; // use `long` so r*r is calculated as a `long`
        while (r*r > x) {
            r = (r + x/r) / 2;
        }    	
        return (int) r;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(log n)
- Space Complexity: O(1)


# Links

- [Discuss on LeetCode](https://leetcode.com/problems/sqrtx/discuss/453059)
- [github.com/RodneyShag](https://github.com/RodneyShag)
