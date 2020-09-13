### Notes

- Leetcode lists the difficulty as _Easy_ for this question. This question is only easy if you solve it using a brute-force technique.
- The below algorithm is the famous "KMP" linear-time solution algorithm. I would classify this question _Hard_ as it may take 1 hour to understand this algorithm before coding.

### Algorithm

1. We must first create a "Longest Prefix Suffix" array, where for each position in our "needle", we see if there's a prefix that matches a suffix
    - [Video example 1](https://youtu.be/V5-7GzOfADQ?t=461) - watch from 7:41 to 11:58
    - [Video example 2](https://youtu.be/GTJr8OvyEVQ?t=332) - watch from 5:33 to 10:14
1. Use this array (along with very similar code structure & logic), to calculate strStr()
    - [Video example](https://youtu.be/GTJr8OvyEVQ?t=620) - watch from 10:20 to 12:28

### Solution

```java
class Solution {
  private int[] computeLPS(String str) { // computes Longest Prefix Suffix (LPS) array
    int[] lps = new int[str.length()];
    lps[0] = 0;
    int i = 1; // always walks forward
    int j = 0; // tracks prefix that matches suffix

    while (i < str.length()) {
      if (str.charAt(i) == str.charAt(j)) {
        j++;
        lps[i] = j;
        i++;
      } else { // mismatch
        if (j == 0) { // go onto next character in string
          lps[i] = 0;
          i++;
        } else { // backtrack j to check previous matching prefix
          j = lps[j - 1];
        }
      }
    }
    return lps;
  }

  int strStr(String haystack, String needle) {
      if (haystack == null || needle == null || haystack.length() < needle.length()) {
          return -1;
      } else if (needle.isEmpty()) {
          return 0;
      }

      int[] lps = computeLPS(needle);
      int i = 0;
      int j = 0;

      while (i < haystack.length()) {
          if (needle.charAt(j) == haystack.charAt(i)) {
              i++;
              j++;
              if (j == needle.length()) {
                  return i - j; // match found. Return location of match
              }
          } else {
              if (j == 0) {
                  i++;
              } else {
                  j = lps[j - 1]; // backtrack j to check previous matching prefix
              }
          }
      }

      return -1; // did not find needle
  }
}
```

### Time/Space Complexity

- Time Complexity: O(m+n)
  - O(m) is to build the "LPS" array
  - O(n) is the while loop in `strStr()`. Tricky: In the while loop, in the last `else`, when we don't do `i++`, notice `j` backtracks an __amortized__ time of once for each increment of `i`.
- Space Complexity: O(m)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
