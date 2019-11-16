### Algorithm

- Represent the T9 numberpad as a `HashMap<Character, String>`
- Use "Backtracking" - an algorithm for finding all solutions by exploring all potential candidates.
  - For the 0th digit, we will have 3-4 choices of letters, so we will try each one.
  - For the 1st digit, we will have 3-4 choices of letters, so we will try each one.
  - ...
  - For the last digit, we will have 3-4 choices of letters, so we will try each one.
- We represent the above logic using recursion where each choice of letter is represented by a separate recursive call
- We will use a `StringBuffer` to keep track of our choice of letters so far

### Solution

```java
class Solution {
    Map<Character, String> map = new HashMap<Character, String>() {{
        put('2', "abc");
        put('3', "def");
        put('4', "ghi");
        put('5', "jkl");
        put('6', "mno");
        put('7', "pqrs");
        put('8', "tuv");
        put('9', "wxyz");
    }};

    public List<String> letterCombinations(String digits) {
        if (digits == null || digits.length() == 0) {
            return new ArrayList<>();
        }
        List<String> solutions = new ArrayList<>();
        makeStrings(digits, 0, solutions, new StringBuffer());
        return solutions;
    }

    private void makeStrings(String digits, int index, List<String> solutions, StringBuffer sb) {
        if (index == digits.length()) {
            solutions.add(sb.toString());
            return;
        }
        char digit = digits.charAt(index);
        String letters = map.get(digit);
        for (char letter : letters.toCharArray()) {
            sb.append(letter);
            makeStrings(digits, index + 1, solutions, sb);
            sb.deleteCharAt(sb.length() - 1);   
        }
    }
}
```

### Time/Space Complexity

Let `M`  be the number of digits in the input that maps to 3 letters (digits 2, 3, 4, 5, 6, 8) and `N` be the number of digits in the input that maps to 4 letters (digits 7, 9), where `M + N` is the total number of digits in the input.

There will be 3<sup>M</sup> * 4<sup>N</sup> solutions, and each one will take O(M+N) time to copy into our `solutions`

-  Time Complexity: O((M+ N) * 3<sup>M</sup> * 4<sup>N</sup>)
- Space Complexity: O((M+ N) * 3<sup>M</sup> * 4<sup>N</sup>)

### Similar BackTracking Problems

- [Permutations](https://leetcode.com/problems/permutations) and [Permutations II](https://leetcode.com/problems/permutations-ii)
- [Subsets](https://leetcode.com/problems/subsets) and [Subsets II](https://leetcode.com/problems/subsets-ii)
- [N-Queens](https://leetcode.com/problems/n-queens)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/discuss/313425)
- [github.com/RodneyShag](https://github.com/RodneyShag)
