### Algorithm

Let's calculate the _depth_ of a tree for a root `TreeNode`. The [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree) problem has a [solution](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Maximum%20Depth%20of%20Binary%20Tree.md) that shows how to do this.

If at a root node (without using parents), the diameter is the maximum of either:
1. Max depth for Left Subtree + max depth for right subtree
1. Diameter of Left subtree (without using this `TreeNode`)
1. Diameter of Right subtree (without using this `TreeNode`)

We visit every `TreeNode` recursively and calculate (1), saving the largest value we've found in `max`. Since we calculate this value for every `TreeNode`, we have indirectly calculated (2) and (3) as well. Our solution is the final value for `max`.

### Provided Code

```java
class TreeNode {
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
    private int max = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        maxDepth(root);
        return max;
    }

    private int maxDepth(TreeNode root) { // defines 1-TreeNode tree to have depth 1
        if (root == null) {
            return 0;
        }
        int L = maxDepth(root.left);
        int R = maxDepth(root.right);
        max = Math.max(max, L + R); // 'L+R' is diameter: L to root to R
        return 1 + Math.max(L, R);
    }
}
```

### Implementation Notes

For `max`, we used a global instance variable. Alternatively, you can [wrap the variable up in an array](https://leetcode.com/problems/diameter-of-binary-tree/discuss/101130/C%2B%2B-Java-Clean-Code) (or class) so changing its value is preserved between function calls.

### Time/Space Complexity

-  Time Complexity: O(n) since we must visit each node.
- Space Complexity: O(log n) if balanced tree, O(n) otherwise. Space complexity is due to the recursion.
