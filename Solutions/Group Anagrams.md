# Solution 1 - Sorting

### Algorithm

- If 2 strings are sorted, and their sorted values are equal, they are anagrams.
- Create a HashMap:
  - key -   the sorted version of the String.
  - value - all the unsorted Strings that sort to the key.

### Code

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] array) {
        if (array == null || array.length == 0) {
            return new ArrayList();
        }

        Map<String, List<String>> map = new HashMap();

        for (String str : array) {
            String key = sortChars(str);
            map.putIfAbsent(key, new ArrayList<String>());
            List<String> anagrams = map.get(key);
            anagrams.add(str);
        }

        return new ArrayList(map.values());
    }

    private String sortChars(String str) {
        char[] content = str.toCharArray(); // Strings are immutable, so we convert to char[]
        Arrays.sort(content);
        return new String(content);
    }
}
```

### Time/Space Complexity

- Time Complexity: O(nk log k), where `n` is the number of strings, and `k` is the length of the longest string.
- Space Complexity: O(nk) for storing the strings.


# Solution 2 - Character Counts

### Algorithm

- In our above solution, we were using sorting (O(n log n)) to see if 2 strings are anagrams. Instead, we can compare the letter counts of the Strings to see if they're anagrams (O(n))
- The only difference in this solution is how we create the key for our `HashMap`. Our key will represent the number of letters in each string, where each letter is associated with a count. We can use a `Map<Character, Integer>` to represent this key.

### Code

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] array) {
        if (array == null || array.length == 0) {
            return new ArrayList();
        }

        Map<Map<Character, Integer>, List<String>> map = new HashMap();

        for (String str : array) {
            Map<Character, Integer> key = createKey(str);
            map.putIfAbsent(key, new ArrayList<String>());
            List<String> anagrams = map.get(key);
            anagrams.add(str);
        }

        return new ArrayList(map.values());
    }

    private Map<Character, Integer> createKey(String str) {
        Map<Character, Integer> key = new HashMap();
        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);
            key.merge(ch, 1, Integer::sum);
        }
        return key;
    }
}
```

### Notes

- If you don't like using a `Map<Character, Integer>` as a key, you can convert this to a `String`, using a separator (such as a hyphen `-`, or any non-digit character) between the counts. So `bad` would be `1-1-0-1-...0-`, where the `...` are the remaining 21 letters.

### Time/Space Complexity

- Time Complexity: O(nk), where `n` is the number of strings, and `k` is the length of the longest string.
- Space Complexity: O(nk) for storing the strings.

# Links

- [Discuss on LeetCode](https://leetcode.com/problems/group-anagrams/discuss/308683)
- [github.com/RodneyShag](https://github.com/RodneyShag)
