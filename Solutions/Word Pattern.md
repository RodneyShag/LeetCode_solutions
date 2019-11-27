### Algorithm

1. Since spaces are not part of the pattern, we split our string on spaces and save it as an array of words.
1. Loop through each ith character in `pattern`, and compare it with ith word.
    - Save these `Character` to `String` mappings in `map1`.
    - Due to "bijection" requirement in problem, where 2 Characters can't map to same word, we will store `String` to `Character` mappings in `map2`.
    - If at any time during the loop we violate any pattern-matching or bijection principles, return false.

### Solution

```java
class Solution {
    public boolean wordPattern(String pattern, String str) {
        if (pattern == null || str == null || pattern.length() == 0 || str.length() == 0) {
            return false;
        }
        String[] words = str.split(" ");
        if (words.length != pattern.length()) {
            return false;
        }

        Map<Character, String> map1 = new HashMap();
        Map<String, Character> map2 = new HashMap();

        for (int i = 0; i < pattern.length(); i++) {
            char ch = pattern.charAt(i);
            if (map1.containsKey(ch) && !map1.get(ch).equals(words[i])) {
                return false;
            } else if (map2.containsKey(words[i]) && map2.get(words[i]) != ch) {
                return false; // due to "bijection" requirement in problem
            }
            map1.put(ch, words[i]);
            map2.put(words[i], ch);
        }
        return true;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/word-pattern/discuss/326764)
- [github.com/RodneyShag](https://github.com/RodneyShag)
