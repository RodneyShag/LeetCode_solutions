### Notes

- Our standard number system has digits 0 to 9, which is a _base 10_ system.
- In this problem we have letters A to Z, so we would like to say this is a _base 26_ system. However,  we have no way to represent 0, so the analogy to a "base something" system cannot be made.

### Solution

```java
class Solution {
    public int titleToNumber(String s) {
        if (s == null) {
            return -1;
        }
        int num = 0;
        for (int i = 0; i < s.length(); i++) {
            num *= 26; // 26 possible letters
            num += s.charAt(i) - 'A' + 1;
        }
        return num;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

# Links

- [Discuss on LeetCode](https://leetcode.com/problems/excel-sheet-column-number/discuss/442118)
- [github.com/RodneyShag](https://github.com/RodneyShag)
