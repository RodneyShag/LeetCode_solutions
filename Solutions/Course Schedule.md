### Notes

- Algorithm is from Jeff Erickson's Algorithms.pdf, Section 19.5 Topological Sort.
- The [general solution](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Course%20Schedule%20II.md) returns the topological order. The solution below modifies the general solution to return just true/false.

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
        neighbors = new ArrayList();
    }

    public void addDirectedNeighbor(Node neighbor) {
        neighbors.add(neighbor);
    }
}
```

```java
class Graph {
    List<Node> nodes = new ArrayList();
    Map<Integer, Node> map = new HashMap();

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
    public boolean canFinish(int numCourses, int[][] prerequisites) {
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

    private boolean topoSort(Graph graph) {
        Node source = new Node(-1);
        for (Node node : graph.nodes) {
            source.addDirectedNeighbor(node);
        }
        try {
            topoSortDFS(source);
        } catch (Exception e) {
            return false;
        }
        return true;
    }

    private void topoSortDFS(Node n) throws Exception {
        n.status = Visited.ACTIVE;
        for (Node neighbor : n.neighbors) {
            if (neighbor.status == Visited.NEW) {
                topoSortDFS(neighbor);
            } else if (neighbor.status == Visited.ACTIVE) {
                throw new Exception("Not a Directed Acyclic Graph (DAG). Graph has a cycle.");
            }
        }
        n.status = Visited.DONE;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n) due to recursion

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/course-schedule/discuss/304362)
- [github.com/RodneyShag](https://github.com/RodneyShag)
