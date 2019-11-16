### Notes

Algorithm is from Jeff Erickson's Algorithms.pdf, Section 19.5 Topological Sort

### Solution

```java
enum Visited {
    NEW, ACTIVE, DONE
}
```

```java
class Node {
    int data;
    Visited status;
    List<Node> neighbors; // could alternatively use a HashSet (if I give nodes unique IDs)

    public Node(int data) {
        this.data = data;
        status = Visited.NEW;
        neighbors = new ArrayList<>();
    }

    public void addDirectedNeighbor(Node neighbor) {
        neighbors.add(neighbor);
    }
}
```

```java
class Graph {
    List<Node> nodes = new ArrayList<>();
    Map<Integer, Node> map = new HashMap<>();

    public void addDirectedEdge(Integer s1, Integer s2) {
        Node source = map.get(s1);
        Node destination = map.get(s2);
        source.addDirectedNeighbor(destination);
    }

    public void addNode(Integer data) {
        Node node = new Node(data);
        nodes.add(node);
        map.put(data, node);
    }
}
```

```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        // Create Graph
        Graph graph = new Graph();
        for (int i = 0; i < numCourses; i++) {
            graph.addNode(i);
        }
        for (int[] prereq : prerequisites) {
            // prereq[1] is the prerequisite to prereq[0]
            int destination = prereq[0];
            int source = prereq[1];
            graph.addDirectedEdge(source, destination);
        }

        return topoSort(graph);
    }

    private int[] topoSort(Graph graph) {
        Node source = new Node(-1);
        for (Node node : graph.nodes) {
            source.addDirectedNeighbor(node);
        }

        ArrayDeque<Node> result = new ArrayDeque<>();
        try {
            topoSortDFS(source, result);
        } catch (Exception e) {
            return new int[0];
        }
        result.removeFirst(); // removes the source node we created
        return convertToArray(result);
    }

    private void topoSortDFS(Node n, ArrayDeque<Node> result) throws Exception {
        n.status = Visited.ACTIVE;
        for (Node neighbor : n.neighbors) {
            if (neighbor.status == Visited.NEW) {
                topoSortDFS(neighbor, result);
            } else if (neighbor.status == Visited.ACTIVE) {
                throw new Exception("Not a Directed Acyclic Graph (DAG). Graph has a cycle.");
            }
        }
        n.status = Visited.DONE;
        result.addFirst(n);
    }

    private int[] convertToArray(ArrayDeque<Node> deque) {
        int[] array = new int[deque.size()];
        int i = 0;
        while (!deque.isEmpty()) {
            array[i] = deque.removeFirst().data;
            i++;
        }
        return array;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n) due to recursion

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/course-schedule-ii/discuss/304370)
- [github.com/RodneyShag](https://github.com/RodneyShag)
