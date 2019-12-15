This is very similar to the [Power of Three](https://leetcode.com/problems/power-of-three) question on LeetCode.

# Solution 1 - Using Loop

### Algorithm

If a number is a power of 4, we can keep dividing it by 4 until we end up with a value of 1.

### Code

```java
class Solution {
    public boolean isPowerOfFour(int n) {
        if (n < 1) {
            return false;
        }
        while (n % 4 == 0) {
            n /= 4;
        }
        return n == 1;
    }
}
```

### Notes

This algorithm works for any "Power of X" question for X = 2, 3, 4,...

### Time/Space Complexity

- Time Complexity: O(1)
- Space Complexity: O(1)


# Solution 2 - Base Conversion

### Algorithm

1. Convert the number to base-4 representation.
1. Check if it starts with `1` (and followed by 0 or more 0s)

### Code

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        return Integer.toString(n, 4).matches("10*");
    }
}
```

### Notes

This algorithm works for any "Power of X" question for X = 2, 3, 4,...

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

# Links

- [Discuss on LeetCode](https://leetcode.com/problems/power-of-four/discuss/451488)
- [github.com/RodneyShag](https://github.com/RodneyShag)
