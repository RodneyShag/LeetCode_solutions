### Solution

```java
class Solution {
    public String countAndSay(int n) {
        if (n <= 0) {
            return "";
        }
        String s = "1";
        for (int i = 2; i <= n; i++) {
            s = say(s);
        }
        return s;
    }

    private String say(String s) {
        StringBuffer sb = new StringBuffer();
        int count = 1;
        for (int i = 1; i < s.length(); i++) {
            char prev = s.charAt(i - 1);
            char curr = s.charAt(i);
            if (curr == prev) {
                count++;
            } else {
                sb.append(count).append(prev);
                count = 1;
            }
        }
        // append count of last character
        sb.append(count).append(s.charAt(s.length() - 1));

        return sb.toString();
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(nm) where m is the length of the `String` on the last iteration.
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/count-and-say/discuss/457513)
- [github.com/RodneyShag](https://github.com/RodneyShag)
