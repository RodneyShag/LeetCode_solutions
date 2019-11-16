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
    public List<Integer> postorder(Node root) {
        List<Integer> list = new ArrayList<>();
        postorder(root, list);
        return list;
    }

    private void postorder(Node node, List<Integer> list) {
        if (node != null) {
            for (Node n : node.children) {
                postorder(n, list);
            }
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

- [Discuss on LeetCode](https://leetcode.com/problems/n-ary-tree-postorder-traversal/discuss/312432)
- [github.com/RodneyShag](https://github.com/RodneyShag)
