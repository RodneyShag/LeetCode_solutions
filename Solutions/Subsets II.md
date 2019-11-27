### Algorithm

- This is the same question as [the "Subsets" problem](https://leetcode.com/problems/subsets) - Here's [my solution to that problem](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/LeetCode/Subsets.md)
- We will make 2 changes to the solution above to account for removing duplicates
  1. Use a `Set` to remove duplicates. For input [1,1,4] we don't want subset [1,4] to exist twice in our solution
  1. Since we are using a `Set<List<Integer>>`, we will run into a problem if our input set is [1,4,1], as our code will create lists: [1,4] and [4,1]. To prevent this, we will sort our input set [1,4,1] to [1,1,4]. Now our code will create lists [1,4] and [1,4] where one of them will be removed by our `Set`

### Solution

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] array) {
        if (array == null || array.length == 0) {
            return new ArrayList();
        }
        Arrays.sort(array);
        Set<List<Integer>> solutions = new HashSet();
        makeSubsets(array, 0, solutions, new ArrayList());
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

There are 2<sup>n</sup> subsets to generate, and each one takes `O(n)` time to copy the `list` into our `solutions`

-  Time Complexity: O(n * 2<sup>n</sup>)
- Space Complexity: O(n * 2<sup>n</sup>)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/subsets-ii/discuss/324262)
- [github.com/RodneyShag](https://github.com/RodneyShag)
