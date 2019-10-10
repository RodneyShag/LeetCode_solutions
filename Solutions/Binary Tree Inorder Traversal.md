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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        inorderTraversal(root, list);
        return list;
    }

    private void inorderTraversal(TreeNode node, List<Integer> list) {
        if (node != null) {
            inorderTraversal(node.left, list);
            list.add(node.val);
            inorderTraversal(node.right, list);
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) since we must visit all nodes.
- Space Complexity: O(log n) on balanced tree. O(n) otherwise.

### Notes

The follow-up question asks us for an iterative solution, but there is no benefit to that solution as neither the time or space complexity is improved by solving the problem iteratively.
