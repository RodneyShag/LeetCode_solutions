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
    public List<List<Integer>> levelOrder(TreeNode root) {
        if (root == null) {
            return new ArrayList<>();
        }
        List<List<Integer>> lists = new ArrayList<>();
        Deque<TreeNode> deque = new ArrayDeque<>(); // use deque as a queue
        deque.add(root);
        while (!deque.isEmpty()) {
            int numNodesInLevel = deque.size();
            List<Integer> level = new ArrayList<>(numNodesInLevel);
            for (int i = 0; i < numNodesInLevel; i++) {
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

- [Discuss on LeetCode](https://leetcode.com/problems/binary-tree-level-order-traversal/discuss/304507)
- [github.com/RodneyShag](https://github.com/RodneyShag)
