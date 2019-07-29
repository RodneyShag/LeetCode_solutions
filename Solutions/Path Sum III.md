### Algorithm

This is the same problem as [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k), except instead of being in a 1-Dimensional array, it is in a tree.

See [my solution to the above problem](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Subarray%20Sum%20Equals%20K.md), then apply it to this problem.

### Provided code

```java
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) {
        val = x;
    }
}
```

### Solution

```java
class Solution {
    public int pathSum(TreeNode node, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);
        return pathSum(node, target, 0, map);
    }

    private int pathSum(TreeNode node, int target, int sum, Map<Integer, Integer> map) {
        if (node == null) {
            return 0;
        }
        sum += node.val;
        int result = map.getOrDefault(sum - target, 0);

        map.merge(sum, 1, Integer::sum);
        result += pathSum(node.left, target, sum, map);
        result += pathSum(node.right, target, sum, map);
        map.merge(sum, -1, Integer::sum);
        if (map.get(sum) == 0) { // Remove when 0 to reduce space usage
            map.remove(sum);
        }

        return result;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(log n) if balanced tree. O(n) otherwise.
