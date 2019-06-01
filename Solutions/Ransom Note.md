### Algorithm

1. Store `magazine` as `Character`s in a `HashMap` (where `key` is the `Character` and `value` is the count)
1. Loop through `ransomNote` and use the `Character`s in our `HashMap`.

### Solution

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        HashMap<Character, Integer> usableLetters = getLetters(magazine);
        for (int i = 0; i < ransomNote.length(); i++) {
            char letter = ransomNote.charAt(i);
            if (usableLetters.containsKey(letter) && usableLetters.get(letter) > 0) {
                usableLetters.merge(letter, -1, Integer::sum); // uses the letter
            } else {
                return false;
            }
        }
        return true;
    }

    private HashMap<Character, Integer> getLetters(String magazine) {
        HashMap<Character, Integer> letters = new HashMap<>();
        for (int i = 0; i < magazine.length(); i++) {
            letters.merge(magazine.charAt(i), 1, Integer::sum);
        }
        return letters;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n + m)
- Space Complexity: O(m) to store `magazine` in a `HashMap` of characters
