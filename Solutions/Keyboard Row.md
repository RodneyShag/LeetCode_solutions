### Algorithm

Use a "regular expression" (regex) by using [.matches()](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#matches-java.lang.String-).

- `[]` around a 'set' of characters is a match if any of the characters match
- `+` means 1 or more of whatever precedes it. We can alternatively use `*` which means 0 or more.
- `|` means "or"

### Solution

```java
class Solution {
    public String[] findWords(String[] words) {
        if (words == null) {
            return null;
        }
        List<String> list = new ArrayList();
        for (String word : words) {
            if (word.toLowerCase().matches("[qwertyuiop]+|[asdfghjkl]+|[zxcvbnm]+")) {
                list.add(word);
            }
        }
        return list.toArray(new String[list.size()]);
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) where n is the number of words
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/keyboard-row/discuss/459920)
- [github.com/RodneyShag](https://github.com/RodneyShag)
