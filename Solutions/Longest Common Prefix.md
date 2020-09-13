### Algorithm

We will compare the `i = 0` character of all the words, then `i = 1, 2, 3....`

```
     i: 012345
        ------
        flower
        flow
        flight
        ------
prefix: fl____
```

### Solution

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        for (int i = 0; i < strs[0].length() ; i++){
            char c = strs[0].charAt(i);
            for (int j = 1; j < strs.length; j++) {
                if (i == strs[j].length() || strs[j].charAt(i) != c) {
                    return strs[0].substring(0, i);
                }
            }
        }
        return strs[0];
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(s) where s is sum of all characters in all strings
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
