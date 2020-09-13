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

- [github.com/RodneyShag](https://github.com/RodneyShag)
