### Provided Code

```java
class TreeNode {
    TreeNode left;
    TreeNode right;
}
```

### Solution

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        TreeNode  left = invertTree(root.left);
        TreeNode right = invertTree(root.right);
        root.left = right;
        root.right = left;
        return root;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) since we must visit every TreeNode.
- Space Complexity: O(log n) if balanced tree. O(n) otherwise.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/invert-binary-tree/discuss/401523)
- [github.com/RodneyShag](https://github.com/RodneyShag)
