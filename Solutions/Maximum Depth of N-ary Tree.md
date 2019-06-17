### Notes

This problem defines a 1-TreeNode tree to have height of 1.

### Provided code

```java
class Node {
    int val;
    List<Node> children;
}
```

### Solution

```java
class Solution {
    public int maxDepth(Node root) {
        if (root == null) {
            return 0;
        }
        int max = 0;
        for (Node child : root.children) {
            max = Math.max(max, maxDepth(child));
        }
        return 1 + max;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n) since we must touch all nodes
- Space Complexity: O(n) due to recursion (on a tree that may not be balanced)
