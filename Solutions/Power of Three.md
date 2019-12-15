# Solution 1 - Using Loop

### Algorithm

If a number is a power of 3, we can keep dividing it by 3 until we end up with a value of 1.

### Code

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        if (n < 1) {
            return false;
        }
        while (n % 3 == 0) {
            n /= 3;
        }
        return n == 1;
    }
}
```

### Notes

This algorithm works for any "Power of X" question for X = 2, 3, 4,...


### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

# Solution 2 - Base Conversion

### Algorithm

1. Convert the number to base-3 representation.
1. Check if it starts with `10`

### Code

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        return Integer.toString(n, 3).matches("10*");
    }
}
```

### Notes

This algorithm works for any "Power of X" question for X = 2, 3, 4,...

### Time/Space Complexity

- Time Complexity: O(1)
- Space Complexity: O(1)


# Solution 3 - Integer Limitations

### Algorithm

This algorithm only works since 3 is a prime number.

1. 3<sup>19</sup> = 1162261467 is the biggest power of 3 less than `Integer.MAX_VALUE`.
1. Since 3 is a prime number, the only divisors of 3<sup>19</sup> are 3<sup>0</sup>, 3<sup>1</sup>, 3<sup>2</sup>, ... 3<sup>19</sup>, which happen to all be powers of 3.
1. Return `true` if `n` is positive and `1162261467` is divisible by `n`

### Code

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        return n > 0 &&
               1162261467 % n == 0;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(1)
- Space Complexity: O(1)


# Links

- [Discuss on LeetCode](https://leetcode.com/problems/power-of-three/discuss/448777)
- [github.com/RodneyShag](https://github.com/RodneyShag)
