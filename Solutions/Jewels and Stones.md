### Algorithm

1. Put jewels in a `Set` for O(1) access.
1. For each stone, check if it is a jewel.

### Solution

```java
class Solution {
    public int numJewelsInStones(String j, String s) {
        Set<Character> jewels = new HashSet();
        for (int i = 0; i < j.length(); i++) {
            jewels.add(j.charAt(i));
        }
        int count = 0;
        for (int i = 0; i < s.length(); i++) {
            if (jewels.contains(s.charAt(i))) {
                count++;
            }
        }
        return count;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(j + s)
- Space Complexity: O(j)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/jewels-and-stones/discuss/457539)
- [github.com/RodneyShag](https://github.com/RodneyShag)
