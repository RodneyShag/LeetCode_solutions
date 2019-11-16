### Tips

1. We can't simply multiply out n! and count number of 0s since n! may be too big to fit in an int/long.
1. Trailing 0's are created by 2's and 5's. Since we will always have more 2's than 5's, the 5's will determine # of 0's.
1. 1 solution is to count # of factors of 5's in each term of the factorial (1...n), however, this is a time-intensive solution
1. Instead, count multiples of 5 (btwn 1 and n), then multiples of 25, then 125... using a `for` loop that gives us `n/5 + n/25 + n/125 + n/625  + ...;`


```
Special numbers:
  5   = 5
  25  = 5 x 5
  125 = 5 x 5 x 5
  625 = 5 x 5 x 5 x 5
```

### Solution
```java
int numTrailingZeros(int n) {
    if (n < 1) {
        return 0;
    }
    int fives = 0;
    for (long i = 5; i <= n; i *= 5) { // i is 5, 25, 125, 625 ...
        fives += n/i; // to count how many multiples of "i" are in range 1...n, we just do n/i
    }
    return fives;
}
```

### Implementation Notes

Must use `long i` to prevent integer overflow from the `i *= 5`

### Time/Space Complexity

-  Time Complexity: O(log n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/factorial-trailing-zeroes/discuss/313449)
- [github.com/RodneyShag](https://github.com/RodneyShag)
