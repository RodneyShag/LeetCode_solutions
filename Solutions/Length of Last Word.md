### Solution

```java
class Solution {
    public int lengthOfLastWord(String s) {
        if (s == null) {
            return 0;
        }
        s = s.trim();
        for (int i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) == ' ') {
                return s.length() - 1 - i;
            }
        }
        return s.length();
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

# Links

- [Discuss on LeetCode](https://leetcode.com/problems/length-of-last-word/discuss/458364)
- [github.com/RodneyShag](https://github.com/RodneyShag)
