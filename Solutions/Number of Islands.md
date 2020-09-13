# Algorithm

- Loop through our `char[][] grid`, and for each piece of land we see (a `1`), we mark all the land it's connected to.
  - Can use either Depth-First Search (DFS) or Bread-First Search (BFS) to find connected land.
- We mark land by simply changing the `1` in our `grid` to a `0`.

# Solution - Depth-First Search (DFS)

### Solution

```java
class Solution {
    private int rows;
    private int cols;

    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
        rows = grid.length;
        cols = grid[0].length;
        int count = 0;

        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (grid[r][c] == '1') {
                    explore(grid, r, c);
                    count++;
                }
            }
        }
        return count;
    }

    // Depth-First Search (DFS)
    private void explore(char[][] grid, int r, int c) {
        if (r < 0 || r >= rows || c < 0 || c >= cols || grid == null || grid[r][c] == '0') {
            return;
        }

        grid[r][c] = '0'; // we alter the original matrix here

        // Recursively search neighbors
        explore(grid, r - 1, c);
        explore(grid, r + 1, c);
        explore(grid, r, c - 1);
        explore(grid, r, c + 1);
    }
}
```

### Time/Space Complexity

- Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols) due to recursion


# Alternate Solution - BFS

You only need to be aware of this alternate solution if you are the interviewer.

Solving with BFS requires more code, mostly due to the creation of the `Coordinate` class below.

### Code

```java
class Solution {
    private int rows;
    private int cols;

    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
        rows = grid.length;
        cols = grid[0].length;
        int count = 0;

        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (grid[r][c] == '1') {
                    explore(grid, r, c);
                    count++;
                }
            }
        }
        return count;
    }

    // Breadth-First Search (BFS)
    private void explore(char[][] grid, int r, int c) {
        if (!inGrid(grid, r, c) || grid[r][c] == '0') {
            return;
        }

        Deque<Coordinate> deque = new ArrayDeque(); // use deque as a queue
        grid[r][c] = '0'; // we alter the original matrix here
        deque.add(new Coordinate(r, c));

        while (!deque.isEmpty()) {
            Coordinate curr = deque.removeFirst();

            for (Coordinate neighbor : curr.getNeighbors()) {
                if (inGrid(grid, neighbor.r, neighbor.c) && grid[neighbor.r][neighbor.c] == '1') {
                    grid[neighbor.r][neighbor.c] = '0';
                    deque.addLast(neighbor);
                }
            }
        }
    }

    private boolean inGrid(char[][] grid, int r, int c) {
        return grid != null && r >= 0 && r < rows && c >= 0 && c < cols;
    }
}
```

```java
class Coordinate {
    int r;
    int c;

    Coordinate(int r, int c) {
        this.r = r;
        this.c = c;
    }

    List<Coordinate> getNeighbors() {
        List<Coordinate> neighbors = new ArrayList();
        neighbors.add(new Coordinate(r, c + 1)); // right
        neighbors.add(new Coordinate(r, c - 1)); // left
        neighbors.add(new Coordinate(r + 1, c)); // up
        neighbors.add(new Coordinate(r - 1, c)); // down
        return neighbors;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols)

# Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
