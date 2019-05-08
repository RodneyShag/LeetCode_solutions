### Notes

- This problem defines a 1-TreeNode tree to have height of 1.

### Provided code

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}
```

### Solution

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        } else {
            return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
        }
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n) since we must touch all nodes
- Space Complexity: O(n) due to recursion (on a tree that may not be balanced)
