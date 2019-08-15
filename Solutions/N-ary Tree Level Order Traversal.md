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
    public List<List<Integer>> levelOrder(Node root) {
        if (root == null) {
            return new ArrayList<>();
        }
        List<List<Integer>> lists = new ArrayList<>();
        Deque<Node> deque = new ArrayDeque<>(); // use deque as a queue
        deque.add(root);
        while (!deque.isEmpty()) {
            int numNodesInLevel = deque.size();
            List<Integer> level = new ArrayList<>(numNodesInLevel);
            for (int i = 0; i < numNodesInLevel; i++) {
                Node n = deque.remove();
                level.add(n.val);
                for (Node child : n.children) {
                    if (child != null) {
                        deque.add(child);
                    }
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
