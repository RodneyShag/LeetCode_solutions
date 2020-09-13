### Algorithm

Use a "regular expression" (regex) by using [.matches()](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#matches-java.lang.String-).

- `[]` around a 'set' of characters is a match if any of the characters match.
    - `[A-Z]` matches any character from A to Z.
- `*` means 0 or more of whatever precedes it
- `|` means "or"
- `.` matches any character

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

- [github.com/RodneyShag](https://github.com/RodneyShag)
