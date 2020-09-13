### Algorithm

- A tree is a mirror image of itself if its left and right subtrees are mirror images of each other.
- Two trees are mirror images of each other if:
    1. Their roots are equal
    1. The left subtree of `tree1` is a mirror image of the right subtree of `tree2`
    1. The right subtree of `tree1` is a mirror image of the left subtree of `tree2`

### Provided Code

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
    public boolean isSymmetric(TreeNode root) {
        return isMirror(root, root);
    }

    private boolean isMirror(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) {
            return true;
        } else if (t1 == null || t2 == null) {
            return false;
        } else {
            return t1.val == t2.val &&
                   isMirror(t1.left, t2.right) &&
                   isMirror(t1.right, t2.left);
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) since we visit each `TreeNode` once
- Space Complexity: O(log n) for a balanced tree, O(n) otherwise. The space complexity is due to recursion.

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
