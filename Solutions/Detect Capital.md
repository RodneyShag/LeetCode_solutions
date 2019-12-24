### Algorithm

Use a "regular expression" (regex) by using [.matches()](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#matches-java.lang.String-).

- `[]` around a 'set' of characters is a match if any of the characters match
- `*` means 0 or more of whatever precedes it
- `|` means "or"

### Solution

```java
class Solution {
    public boolean detectCapitalUse(String word) {
        if (word == null) {
            return false;
        }
        return word.matches("[A-Z]*|.[a-z]*");
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/detect-capital/discuss/460102)
- [github.com/RodneyShag](https://github.com/RodneyShag)
