### Notes from Problem Statement

- "A node is a descendant of itself"
- "All node values are unique"
- "`p` and `q` are different and both values will exist in the BST"

### Algorithm

- Notice we have a binary __search__ tree. That means the numbers are ordered.
- Traverse down the tree. At each node:
    - if the node's value is smaller than both `p` and `q`, go right
    - if it's bigger, go left
    - otherwise, we've found the Lowest Common Ancestor


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
        if (root == null || p == null || q == null) {
            return null;
        }
        TreeNode node = root;
        while (node != null) {
            if (node.val < p.val && node.val < q.val) {
                node = node.right;
            } else if (node.val > p.val && node.val > q.val) {
                node = node.left;
            } else {
                return node;
            }
        }
        return null;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(log n) if balanced tree, O(n) otherwise
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/discuss/328209)
- [github.com/RodneyShag](https://github.com/RodneyShag)
