### Algorithm

- This is the same question as [the "Subsets" problem](https://leetcode.com/problems/subsets) - Here's [my solution to that problem](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/LeetCode/Subsets.md)
- We will make 2 minor changes to the solution above to account for removing duplicates
  1. Sort the input array. This will ensure subsets [4, 1, 4] and [1, 4, 4] are the same set (since they're sorted to be [1, 4, 4])
  1. Use a `Set` to remove duplicates. We don't want [1, 1, 4] to exist twice in our input set


### Solution

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] array) {
        if (array == null || array.length == 0) {
            return new ArrayList<>();
        }
        Arrays.sort(array);
        Set<List<Integer>> solutions = new HashSet<>();
        makeSubsets(array, 0, solutions, new ArrayList<>());
        return new ArrayList<>(solutions);
    }

    private void makeSubsets(int[] array, int i, Set<List<Integer>> solutions, List<Integer> list) {
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
