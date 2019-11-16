### Algorithm

1. Since Java Strings are immutable, convert the String to a char[]
1. Reverse entire String
1. Reverse each word

### Solution

```java
class Solution {
    public String reverseWords(String str) {
        if (str == null) {
            return null;
        }

        char[] sentence = str.trim().replaceAll(" +", " ").toCharArray();
        reverse(sentence, 0, sentence.length - 1);

        int startOfWord = 0;
        for (int i = 0; i < sentence.length; i++) {
            if (sentence[i] == ' ') {
                reverse(sentence, startOfWord, i - 1);
                startOfWord = i + 1;
            }
        }
        reverse(sentence, startOfWord, sentence.length - 1); // reverse last word

        return String.valueOf(sentence);
    }

    private void reverse(char[] array, int start, int end) {
        if (array == null || start < 0 || start >= array.length || end < 0 || end >= array.length) {
            return;
        }
        while (start < end) {
            swap(array, start++, end--);
        }
    }

    private void swap(char[] array, int i, int j) {
        char temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n) - but would be O(1) if we were given a char[] (instead of a String) as input.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/reverse-words-in-a-string/discuss/304479)
- [github.com/RodneyShag](https://github.com/RodneyShag)
