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

- One way to represent the space complexity is `O(nm)` where `m` is the length of the `String` on the last iteration.
- However, `m` is not part of the input, and we want to write space complexity in terms of just the input, which is `n`.
- `m` depends on `n`. In the worst case, `m` doubles in size whenever the previous string does not have 2 adjacent digits that are the same. For example, when `n = 3`, we have `21`, and on `n = 4`, we have `1211`.
- Since m = 2<sup>n</sup> in the worst case, we rewrite the space complexity as O(nm) = O(n2<sup>n</sup>)

### Space Complexity

O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
