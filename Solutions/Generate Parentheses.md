### Algorithm

- Use "Backtracking" - an algorithm for finding all solutions by exploring all potential candidates.
- While building our `expression` left to right, for every index `i`, we must ensure the number of right parenthesis never exceed the number of left parenthesis in the range [0, i]

### Solution

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> solutions = new ArrayList<>();
        addParenthesis(new char[n * 2], 0, n, n, solutions);
        return solutions;
    }

    private void addParenthesis(char[] expression, int index, int leftRem, int rightRem, List<String> solutions) {
        if (leftRem == 0 && rightRem == 0) {
            solutions.add(new String(expression));
            return;
        }
        if (leftRem > 0) {
            expression[index] = '(';
            addParenthesis(expression, index + 1, leftRem - 1, rightRem, solutions);
        }
        if (rightRem > 0 && rightRem > leftRem) {
            expression[index] = ')';
            addParenthesis(expression, index + 1, leftRem, rightRem - 1, solutions);
        }
    }
}
```

### Implementation Details

A `char[]` was used instead of a `StringBuffer` to remove necessity of including a "remove" for every "add" to our expression (when coming out of the recursive call)

### Time/Space Complexity

-  Time Complexity: O(2<sup>n</sup>)
- Space Complexity: O(2<sup>n</sup>)

However, the official LeetCode solutions there is a very difficult mathematical proof to get a tighter bound on the time/space complexity, by using "Catalan" numbers. You are not expected to know this for an interview.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/generate-parentheses/discuss/324390)
- [github.com/RodneyShag](https://github.com/RodneyShag)
