
### Algorithm

[Video explanation](https://www.youtube.com/watch?v=nbTSfrEfo6M) - This is a difficult algorithm.


### Solution

```java
class Solution {
    // Transform s into t.
    // For example, if s = "abba", then t = "$#a#b#b#a#@"
    // the # are interleaved to avoid even/odd-length palindromes uniformly
    // $ and @ are prepended and appended to each end to avoid bounds checking
    private char[] preprocess(String s) {
        char[] t = new char[s.length()*2 + 3];
        t[0] = '$';
        t[s.length()*2 + 2] = '@';
        for (int i = 0; i < s.length(); i++) {
            t[2*i + 1] = '#';
            t[2*i + 2] = s.charAt(i);
        }
        t[s.length()*2 + 1] = '#';
        return t;
    }

    public String longestPalindrome(String s) {
        char[] t = preprocess(s);
        int[] p = new int[t.length];

        int center = 0, right = 0;
        for (int i = 1; i < t.length-1; i++) {
            int mirror = 2 * center - i;

            if (right > i) {
                p[i] = Math.min(right - i, p[mirror]);
            }

            // attempt to expand palindrome centered at i
            while (t[i + (1 + p[i])] == t[i - (1 + p[i])]) {
                p[i]++;
            }

            // if palindrome centered at i expands past right,
            // adjust center based on expanded palindrome.
            if (i + p[i] > right) {
                center = i;
                right = i + p[i];
            }
        }
        return longestPalindromicSubstring(p, s);
    }

    public String longestPalindromicSubstring(int[] p, String s) {
        int length = 0; // length of longest palindromic substring
        int center = 0; // center of longest palindromic substring
        for (int i = 1; i < p.length - 1; i++) {
            if (p[i] > length) {
                length = p[i];
                center = i;
            }
        }
        return s.substring((center - 1 - length) / 2, (center - 1 + length) / 2);
    }
}
```


### Time/Space Complexity

-  Time Complexity: O(n) - but difficult to prove/explain. `i` in the outer for loop moves forward `n` times. The `while` loop does an amortized `O(1)` amount of work.
- Space Complexity: O(n)


### References

- [Code derived from here](https://algs4.cs.princeton.edu/53substring/Manacher.java.html)


### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
