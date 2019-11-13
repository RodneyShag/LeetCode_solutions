### Provided code

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
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) {
            return null;
        } else if (t1 == null) {
            return t2; // keeps entire subtree at t2 intact and returns it.
        } else if (t2 == null) {
            return t1;
        } else {
            TreeNode t = new TreeNode(t1.val + t2.val);
            t.left = mergeTrees(t1.left, t2.left);
            t.right = mergeTrees(t1.right, t2.right);
            return t;
        }
    }
}
```

### Implementation Notes

We reuse nodes from the trees instead of creating new nodes to since this makes merging big subtrees with small subtrees much more efficient.

### Time/Space Complexity

-  Time Complexity: O(n + m) where n is number of nodes in t1, m is number of nodes in t2
- Space Complexity: O(log (n+m)) if balanced tree, O(n + m) otherwise
