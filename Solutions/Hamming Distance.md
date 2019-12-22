### Algorithm

XOR has a value of 1 only when 2 bits are different:

```
XOR

a  b    a ^ b
-------------
0  0      0
0  1      1
1  0      1
1  1      0
```

1. Use XOR as `x ^ y`
1. The number of bits set as `1` in `x ^ y` is our solution

### Solution

```java
class Solution {
    public int hammingDistance(int x, int y) {
        return Integer.bitCount(x ^ y);
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/hamming-distance/discuss/457675)
- [github.com/RodneyShag](https://github.com/RodneyShag)
