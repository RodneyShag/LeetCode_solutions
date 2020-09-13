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
    public List<List<Integer>> levelOrder(TreeNode root) {
        if (root == null) {
            return new ArrayList();
        }
        List<List<Integer>> lists = new ArrayList();
        Deque<TreeNode> deque = new ArrayDeque(); // use deque as a queue
        deque.add(root);
        while (!deque.isEmpty()) {
            int numNodesInLevel = deque.size();
            List<Integer> level = new ArrayList(numNodesInLevel);
            while (numNodesInLevel-- > 0) {
                TreeNode n = deque.remove();
                level.add(n.val);
                if (n.left != null) {
                    deque.add(n.left);
                }
                if (n.right != null) {
                    deque.add(n.right);
                }
            }
            lists.add(level);
        }
        return lists;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
