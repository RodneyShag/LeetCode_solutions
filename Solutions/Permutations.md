### Algorithm

Use "Backtracking" - an algorithm for finding all solutions by exploring all potential candidates.

### Solution

```java
class Solution {
    public List<List<Integer>> permute(int[] array) {
        if (array == null || array.length == 0) {
            return new ArrayList<>();
        }
        List<List<Integer>> solutions = new ArrayList<>();
        permute(array, 0, new boolean[array.length], solutions, new ArrayList<>());
        return solutions;
    }

    private void permute(int[] array, int index, boolean[] used, List<List<Integer>> solutions, List<Integer> list) {
        if (index == array.length) {
            solutions.add(new ArrayList<>(list));
            return;
        }
        for (int i = 0; i < array.length; i++) {
            if (used[i] == false) {
                list.add(array[i]);
                used[i] = true;
                permute(array, index + 1, used, solutions, list);
                used[i] = false;
                list.remove(list.size() - 1);
            }
        }
    }
}
```

### Time/Space Complexity

If you view this recursion as a tree, there will be `n!` leaf nodes, so there are O(n!) nodes in total. At each node, we do O(n) work looping through the array. So our runtime is O(n * n!).

-  Time Complexity: O(n * n!)
- Space Complexity: O(n * n!)

### Similar BackTracking Problems

- [Permutations II](https://leetcode.com/problems/permutations-ii)
- [Subsets](https://leetcode.com/problems/subsets) and [Subsets II](https://leetcode.com/problems/subsets-ii)
- [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number)
- [N-Queens](https://leetcode.com/problems/n-queens)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/permutations/discuss/324282)
- [github.com/RodneyShag](https://github.com/RodneyShag)
