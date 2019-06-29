### Algorithm

- Use "Backtracking" - an algorithm for finding all solutions by exploring all potential candidates.
- Loop through the array, for each index, we have 2 possible "paths" to take.
  1. Don't use the number (and recursively continue)
  1. Use the number (and recursively continue).

### Solution

```java
class Solution {
    public List<List<Integer>> subsets(int[] array) {
        if (array == null || array.length == 0) {
            return new ArrayList<>();
        }
        List<List<Integer>> solutions = new ArrayList<>();
        makeSubsets(array, 0, solutions, new ArrayList<>());
        return solutions;
    }

    private void makeSubsets(int[] array, int i, List<List<Integer>> solutions, List<Integer> list) {
        if (i == array.length) {
            solutions.add(new ArrayList<>(list));
            return;
        }

        // don't use array[i]
        makeSubsets(array, i + 1, solutions, list);

        // use array[i]
        list.add(array[i]);
        makeSubsets(array, i + 1, solutions, list);
        list.remove(list.size() - 1);
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(2<sup>n</sup>)
- Space Complexity: O(2<sup>n</sup>)

These are the fastest complexities that can be achieved as there will always be O(2<sup>n</sup>) subsets to generate

### Similar BackTracking Problems

- [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number)
- [N-Queens](https://leetcode.com/problems/n-queens/)
