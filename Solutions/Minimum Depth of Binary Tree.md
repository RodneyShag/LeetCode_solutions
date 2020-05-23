### Definitions

- This problem defines a 1-TreeNode tree to have a depth of 1.
- "minimum depth" is defined as __the number of nodes along the shortest path from the root node down to the nearest leaf node__.
    - this is a strange definition. Notice it's not the shortest path to a __null__ node, it's the shortest path to a __leaf__ node. In an interview, it's important to verify the exact definition of "minimum depth" before proceeding.

### Examples

The trees below both have a "minimum depth" of 2.

```
      3              1
     / \              \
    9  20              2
      /  \
     15   7
```

### Algorithm

This problem is similar to [LeetCode #104 - Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree). The [solution to that problem](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Maximum%20Depth%20of%20Binary%20Tree.md) uses Depth-First Search (DFS). However, in the problem below we want to find `minDepth()`, so Breadth-First Search (BFS) will be a faster than DFS since it may not need to traverse every node. Implementing BFS on a tree is similar to doing a [level-order traversal on a tree](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Binary%20Tree%20Level%20Order%20Traversal.md)!

### Provided Code

```java
class TreeNode {
    TreeNode left;
    TreeNode right;
}
```

### Solution

```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        Deque<TreeNode> deque = new ArrayDeque(); // use deque as a queue
        deque.add(root);
        int depth = 0;
        while (!deque.isEmpty()) {
            depth++;
            int numNodesInLevel = deque.size();
            while (numNodesInLevel-- > 0) {
                TreeNode n = deque.remove();
                if (n.left == null && n.right == null) {
                    return depth;
                }
                if (n.left != null) {
                    deque.add(n.left);
                }
                if (n.right != null) {
                    deque.add(n.right);
                }
            }
        }
        return depth; // code will never reach here
    }
}
```

### Time/Space Complexity

Let `d` be the "minimum depth" of the tree.

-  Time Complexity: O(2<sup>d</sup>)
- Space Complexity: O(2<sup>d</sup>)

O(2<sup>d</sup>) is faster than O(n) when the tree has some branches that are shorter than others, and we don't visit every node. If the tree is perfectly balanced, then the time/space complexity is O(2<sup>d</sup>) = O(n).

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/minimum-depth-of-binary-tree/discuss/458691)
- [github.com/RodneyShag](https://github.com/RodneyShag)
