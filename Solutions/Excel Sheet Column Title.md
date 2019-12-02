### Notes

- Our standard number system has digits 0 to 9, which is a _base 10_ system.
- In this problem we have letters A to Z, so we would like to say this is a _base 26_ system. However,  we have no way to represent 0, so the analogy to a "base something" system cannot be made.

### Solution

```java
class Solution {
    public String convertToTitle(int n) {
        if (n <= 0) {
            return "";
        }
        StringBuffer sb = new StringBuffer();        
        while (n > 0) {
            sb.insert(0, (char) ('A' + (n - 1) % 26));
            n = (n - 1) / 26;
        }
        return sb.toString();
    }
}
```

### Details Explained

26 represents number of uppercase letters: A to Z.

For the `(char) ('A' + (n - 1) % 26)` in above code:

```
                          n:  1,  2,  3, ... 25, 26, 27, 28 ...
                        n-1:  0,  1,  2, ... 24, 25, 26, 27 ...
                 (n-1) % 26:  0,  1,  2, ... 24, 25,  0,  1 ...
(char) ('A' + (n - 1) % 26):  A,  B,  C, ...  Y,  Z,  A,  B ...
```

For the `(n - 1) / 26`

```
           n:  1,  2,  3, ... 25, 26, 27, 28 ...
(n - 1) / 26:  0,  0,  0, ...  0,  0,  1,  1 ...
```

### Example

Let's use input `28` as an example.

- The `(char) ('A' + (n - 1) % 26)` gives us value `B`.
- The `n = (n - 1) / 26` updates our number to `1`.
- The `(char) ('A' + (n - 1) % 26)` gives us value `A`.
- Our final result is `AB`

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

# Links

- [Discuss on LeetCode](https://leetcode.com/problems/excel-sheet-column-title/discuss/442164)
- [github.com/RodneyShag](https://github.com/RodneyShag)
