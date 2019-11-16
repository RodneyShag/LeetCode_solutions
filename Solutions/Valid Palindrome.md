### Algorithm

1. Create 2 pointers, setting 1 to point to head of list, and 1 to point to tail of list.
1. Skip over any character that's not a letter or digit. Lowercase all characters.
1. If the 2 pointers don't point to equivalent characters, we don't have a palindrome. Otherwise, move the pointers closer to the center of the `String` and repeat steps 2-3 until all characters are checked.
1. If all pairs we checked are equivalent, we have a palindrome.

### Solution

```java
class Solution {
    public boolean isPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }
        int i = 0;
        int j = s.length() - 1;
        while (i < j) {
            if (!Character.isLetterOrDigit(s.charAt(i))) {
                i++;
            } else if (!Character.isLetterOrDigit(s.charAt(j))) {
                j--;
            } else {
                if (Character.toLowerCase(s.charAt(i)) !=
                    Character.toLowerCase(s.charAt(j))) {
                    return false;
                }
                i++;
                j--;
            }
        }
        return true;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/valid-palindrome/discuss/426260)
- [github.com/RodneyShag](https://github.com/RodneyShag)
