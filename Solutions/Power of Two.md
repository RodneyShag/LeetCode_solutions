# Solution 1

### Code

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n < 1) {
            return false;
        }
        return (n & (n - 1)) == 0;
    }
}
```

### Example
Let n = 2^5 = 32. In binary, we have:

```
n           = 00010000
n - 1       = 00001111
n & (n - 1) = 00000000
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)


# Solution 2

### Algorithm

`n` must be positive for it to be a power of 2. It also must have only one 1 bit.

```
 Binary     Decimal
000000001 =    1
000000100 =    4
000010000 =   16
```

### Code

```java
public boolean isPowerOfTwo(int n) {
    if (n < 1) {
        return false;
    }
    return n > 0 && Integer.bitCount(n) == 1;
}
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)


# Links

- [Discuss on LeetCode](https://leetcode.com/problems/power-of-two/discuss/312852)
- [github.com/RodneyShag](https://github.com/RodneyShag)
