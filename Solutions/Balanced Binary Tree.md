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
    public boolean isBalanced(TreeNode root) {
        return isBalancedHelper(root) != -1;
    }

    private int isBalancedHelper(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int leftHeight = isBalancedHelper(root.left);
        if (leftHeight == -1) {
            return -1; // left tree is unbalanced
        }

        int rightHeight = isBalancedHelper(root.right);
        if (rightHeight == -1) {
            return -1; // right tree is unbalanced
        }

        if (Math.abs(leftHeight - rightHeight) > 1) {
            return -1; // imbalance between the 2 subtrees
        }

        return 1 + Math.max(leftHeight, rightHeight);
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(log n) if balanced tree. O(n) otherwise.

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
