### Notes

This problem defines a 1-TreeNode tree to have height of 1.

### Provided code

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
}
```

### Solution

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n) since we must touch all nodes
- Space Complexity: O(n) due to recursion (on a tree that may not be balanced)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree/discuss/304504)
- [github.com/RodneyShag](https://github.com/RodneyShag)
