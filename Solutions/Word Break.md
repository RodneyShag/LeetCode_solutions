# Solution 1 - Dynamic Programming: Recursive

### Details from Problem

"The same word in the dictionary may be reused multiple times in the segmentation." - from problem statement.

You should clarify with your interviewer if words can be reused.

### Algorithm

1. Let `isValid(i)` be a function that determines if a String in range `[0, i)` is a valid document.
1. For `i = 0`, we have the empty string, and this qualifies as a valid document, giving us __true__ as our base case.
1. For a String up to a given index `j`, it is a valid document if we can split the String into 2 parts where
    1. [0, i) is a valid document. (which we can check recursively)
    1. [i, j) is a valid word.
1. For the above step, we will split the string up in `i` possible locations (where `0 <= i < j`) and see if any create a valid document.

### Code

```java
class Solution {
    public boolean wordBreak(String str, List<String> wordDict) {
        Set<String> dict = new HashSet<>(wordDict);
        Map<Integer, Boolean> cache = new HashMap();
        cache.put(0, true); // base case
        return isValid(str, str.length(), dict, cache);
    }

    private boolean isValid(String str, int j, Set<String> dict, Map<Integer, Boolean> cache) {
        Integer key = j;
        if (cache.containsKey(key)) {
            return cache.get(key);
        }
        boolean result = false;
        for (int i = 0; i < j; i++) {
            if (isValid(str, i, dict, cache) && dict.contains(str.substring(i, j))) {
                result = true;
                break;
            }
        }
        cache.put(key, result);
        return result;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(n)


# Solution 2 - Dynamic Programming: Iterative

### Algorithm

- We will use the same logic as in Solution 1, except we will use an array instead of a `HashMap`.
- The tricky part is that we need an array of length `str.length() + 1`. This is because `dp[0]` is our base case (for the empty string), and `dp[str.length()]` represents our final solution for range `[0, str.length())`

### Code

```java
class Solution {
    public boolean wordBreak(String str, List<String> wordDict) {
        Set<String> dict = new HashSet<>(wordDict);
        boolean[] dp = new boolean[str.length() + 1];
        dp[0] = true; // base case
        for (int j = 1; j < dp.length; j++) {
            for (int i = 0; i < j; i++) {
                if (dp[i] && dict.contains(str.substring(i, j))) {
                    dp[j] = true;
                    break;
                }
            }
        }
        return dp[str.length()];
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(n)


# Links

- [Discuss on LeetCode](https://leetcode.com/problems/word-break/discuss/346842)
- [github.com/RodneyShag](https://github.com/RodneyShag)
