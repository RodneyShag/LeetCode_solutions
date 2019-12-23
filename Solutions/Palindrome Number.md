### Algorithm

Convert the `int` to a `String`, and check to see if the `String` is a palindrome.

### Solution

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        String s = String.valueOf(x);
        for (int i = 0; i < s.length() / 2; i++) {
            if (s.charAt(i) != s.charAt(s.length() - 1 - i)) {
                return false;
            }
        }
        return true;
    }
}
```

### Time/Space Complexity

Max size of an `int` in Java is a constant 32 bits, so our `String` length will not exceed 32.

-  Time Complexity: O(1)
- Space Complexity: O(1)

### Follow-up Problem: "Don't use a String"

The `String` solution above is the most efficient and straightforward way to solve this problem. Skip the follow-up.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/palindrome-number/discuss/458320)
- [github.com/RodneyShag](https://github.com/RodneyShag)
