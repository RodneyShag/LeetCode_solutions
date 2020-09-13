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

### Solution 1

If inputs `t1` and `t2` represent immutable trees, we can reuse nodes from these trees instead of creating new nodes. This makes merging big subtrees with small subtrees much more efficient.

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

### Solution 2

If reusing `TreeNode`s is not allowed, we can always create new `TreeNode`s as shown below

```java
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) {
            return null;
        }
        TreeNode t = new TreeNode(
            (t1 == null ? 0 : t1.val) +
            (t2 == null ? 0 : t2.val)
        );
        t.left = mergeTrees(t1 == null ? null : t1.left, t2 == null ? null : t2.left);
        t.right = mergeTrees(t1 == null ? null : t1.right, t2 == null ? null : t2.right);
        return t;
    }
}
```

### Time/Space Complexity (for both solutions)

-  Time Complexity: O(n + m) where n is number of nodes in t1, m is number of nodes in t2
- Space Complexity: O(log (n+m)) if balanced tree, O(n + m) otherwise

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
