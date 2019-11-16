### Algorithm

1. Create HashMap of number frequencies. Frequency = # of times a number appears in array.
1. Create buckets, 1 for each possible frequency. Put a Trie in each bucket. The trie will help us get the words in alphabetical order.
1. To get the most frequent elements, loop through the buckets in descending order.

### Solution

```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        if (words == null || words.length == 0) {
            return Collections.<String>emptyList();
        }

        Map<String, Integer> map = new HashMap<>();
        for (String word : words) {
            map.merge(word, 1, Integer::sum);
        }

        Trie[] buckets = new Trie[words.length + 1];
        for (int i = 0; i < words.length + 1; i++) {
            buckets[i] = new Trie();
        }

        for (String word : map.keySet()) {
            int frequency = map.get(word);
            Trie trie = buckets[frequency];
            trie.add(word);
        }

        List<String> solution = new ArrayList<>();
        for (int i = buckets.length - 1; i >= 0 && solution.size() < k; i--) {
            Trie trie = buckets[i];
            solution.addAll(trie.getWords());
        }
        return solution.subList(0, k);
    }
}
```

```java
class TrieNode {
    public Map<Character, TrieNode> children = new HashMap<>();
    public String word = null;

    public void putChildIfAbsent(char ch) {
        children.putIfAbsent(ch, new TrieNode());
    }

    public TrieNode getChild(char ch) {
        return children.get(ch);
    }
}
```

```java
class Trie {
    private TrieNode root = new TrieNode(); // root wont store any character.

    public void add(String str) {
        TrieNode curr = root;
        for (int i = 0; i < str.length(); i++) {
            Character ch = str.charAt(i);
            curr.putChildIfAbsent(ch);
            curr = curr.getChild(ch);
        }
        curr.word = str;
    }

    public List<String> getWords() {
        List<String> list = new ArrayList<>();
        getWords(root, list);
        return list;
    }

    private void getWords(TrieNode n, List<String> list) {
        if (n.word != null) {
            list.add(n.word);
        }
        for (char child = 'a'; child <= 'z'; child++) {
            if (n.children.containsKey(child)) {
                getWords(n.children.get(child), list);
            }
        }
    }
}
```

### Notes

In the `TrieNode` class, public variables are used for simplicity.

### Time/Space complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/top-k-frequent-words/discuss/304461)
- [github.com/RodneyShag](https://github.com/RodneyShag)
