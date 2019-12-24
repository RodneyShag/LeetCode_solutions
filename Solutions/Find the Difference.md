### Algorithm

If you XOR 2 identical characters by using `^`, you get 0. If we XOR all the characters in the 2 `String`s, all characters that are duplicates will be removed, and we will be left with the only character that occurs once.

### Solution

```java
class Solution {
    public char findTheDifference(String s, String t) { // assumes non-null input
        char c = 0;
        for (int i = 0; i < s.length(); i++) {
            c ^= s.charAt(i);
        }
        for (int i = 0; i < t.length(); i++) {
            c ^= t.charAt(i);
        }
        return c;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(s + t)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/find-the-difference/discuss/460093)
- [github.com/RodneyShag](https://github.com/RodneyShag)
