### Notes from Problem Statement

- "A node is a descendant of itself"
- "All node values are unique"
- "`p` and `q` are different and both values will exist in the BST"

### Algorithm

Notice this is __not a binary search tree__. If it was, it would be equivalent to [this problem](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/), which is simpler to solve.

1. Search left subtree. If we find `p` or `q`, return that node.
1. Search right subtree. If we find `p` or `q`, return that node.
1. If `left` is null, `p` and `q` must be in the right subtree
1. If `right` is null, `p` and `q` must be in the left subtree
1. If neither are null, `p` is on one side, `q` is on other side, so the current node is the lowest common ancestor.

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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        return dfs(root, p, q);
    }

    public TreeNode dfs(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        } else if (root == p || root == q) {
            return root;
        }

        TreeNode left  = dfs(root.left, p, q);
        TreeNode right = dfs(root.right, p, q);

        if (left == null) {
            return right;
        } else if (right == null) {
            return left;
        } else {
            return root;
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) since we may have to search all the nodes.
- Space Complexity: O(log n) if balanced tree, O(n) otherwise. The space complexity is due to recursion.
