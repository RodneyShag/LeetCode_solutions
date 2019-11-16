### Solution

```java
class Solution {
    public int firstUniqChar(String s) {
        if (s == null || s.length() == 0) {
            return -1;
        }

        HashMap<Character, Integer> counts = new HashMap<>();

        // Save counts of characters
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            counts.merge(ch, 1, Integer::sum);
        }

        // Find 1st unique character
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (counts.get(ch) == 1) {
                return i;
            }
        }
        return -1;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1) since we have a finite number of characters (ASCII or Unicode) to store in a `HashMap`

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/first-unique-character-in-a-string/discuss/396406)
- [github.com/RodneyShag](https://github.com/RodneyShag)
