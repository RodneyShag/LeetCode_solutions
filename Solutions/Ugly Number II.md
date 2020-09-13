### Algorithm

This can be viewed as a dynamic programming problem, where the n-th ugly number depends on previous ugly numbers in range [0,n)

If the problem had instead asked for "numbers that have either 2, 3, or 5" as a factor (instead of "__only__ be divided by 2,3,5"), we could create 3 lists (see below) and return the elements in these lists in ascending order.

```
(List 1) Multiples of 2:  1*2, 2*2, 3*2, 4*2, ...
(List 2) Multiples of 3:  1*3, 2*3, 3*3, 4*3, ...
(List 3) Multiples of 5:  1*5, 2*5, 3*5, 4*5, ...
```

For illustration purposes, let's take a look at the ugly numbers:
```
1, 2, 3, 4, 5, 6, 8, 9, 10, 12... (notice that numbers 7, 11 are missing)
```

Since ugly numbers can __only__ be divided by 2, 3, 5, the sequence can be split into 3 groups:
```
(List 1) ugly number sequence * 2:  1*2, 2*2, 3*2, 4*2, 5*2, 6*2, 8*2 ...
(List 2) ugly number sequence * 3:  1*3, 2*3, 3*3, 4*3, 5*3, 6*3, 8*3 ...
(List 3) ugly number sequence * 5:  1*5, 2*5, 3*5, 4*5, 5*5, 6*5, 8*5 ...
```

Use variable `i2`, `i3`, and `i5` to represent which index we are at in each of the above lists, and return the elements in these lists in ascending order

### Solution

```java
class Solution {
    public int nthUglyNumber(int n) {
        if (n < 0) {
            return -1;
        }
        int[] ugly = new int[n];
        ugly[0] = 1;

        int i2 = 0;
        int i3 = 0;
        int i5 = 0;

        for (int i = 1; i < n; i++) {
            ugly[i] = Math.min(ugly[i2] * 2, Math.min(ugly[i3] * 3, ugly[i5] * 5));
            if (ugly[i] == ugly[i2] * 2) {
                i2++;
            }
            if (ugly[i] == ugly[i3] * 3) {
                i3++;
            }
            if (ugly[i] == ugly[i5] * 5) {
                i5++;
            }
        }
        return ugly[n-1];
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

### References

- Solution is from [Geek for Geeks - Ugly Numbers](https://www.geeksforgeeks.org/ugly-numbers/) Method 2, which is also the solution most liked on LeetCode

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
