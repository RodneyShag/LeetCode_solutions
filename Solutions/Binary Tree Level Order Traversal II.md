### Algorithm

- This problem is the same as [LeetCode #102 - Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal) except that it wants the order of the lists reversed
- Use the same [solution to that problem](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Binary%20Tree%20Level%20Order%20Traversal.md), except insert lists into the solution in reverse order
- Since we keep inserting into our list at position 0, we will use a `LinkedList` instead of an `ArrayList` for efficiency

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        if (root == null) {
            return new LinkedList();
        }
        List<List<Integer>> lists = new LinkedList();
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
            lists.add(0, level);
        }
        return lists;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/discuss/458607)
- [github.com/RodneyShag](https://github.com/RodneyShag)
