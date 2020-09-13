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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList();
        postorderTraversal(root, list);
        return list;
    }

    private void postorderTraversal(TreeNode node, List<Integer> list) {
        if (node != null) {
            postorderTraversal(node.left, list);
            postorderTraversal(node.right, list);
            list.add(node.val);
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) since we must visit all nodes.
- Space Complexity: O(log n) on balanced tree. O(n) otherwise.

### Notes

The follow-up question asks us for an iterative solution, but there is no benefit to that solution as neither the time or space complexity is improved by solving the problem iteratively.

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
