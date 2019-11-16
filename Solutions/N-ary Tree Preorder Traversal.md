### Provided Code

```java
public class Node {
    int val;
    List<Node> children;
}
```

### Solution

```java
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> list = new ArrayList<>();
        preorder(root, list);
        return list;
    }

    private void preorder(Node node, List<Integer> list) {
        if (node != null) {
            list.add(node.val);
            for (Node n : node.children) {
                preorder(n, list);
            }
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

- [Discuss on LeetCode](https://leetcode.com/problems/n-ary-tree-preorder-traversal/discuss/312431)
- [github.com/RodneyShag](https://github.com/RodneyShag)
