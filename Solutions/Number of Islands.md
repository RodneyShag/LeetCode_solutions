### Algorithm

- Loop through our `char[][] grid`, and for each piece of land we see (a `1`), we mark all the land it's connected to.
- We mark land by simply changing the `1` in our `grid` to a `0`.

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

        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (grid[row][col] == '1') {
                    explore(grid, row, col);
                    count++;
                }
            }
        }
        return count;
    }

    private void explore(char[][] grid, int row, int col) {
        if (row < 0 || row >= rows || col < 0 || col >= cols || grid == null || grid[row][col] == '0') {
            return;
        }

        grid[row][col] = '0'; // we alter the original matrix here

        // Recursively search neighbors
        explore(grid, row - 1, col);
        explore(grid, row + 1, col);
        explore(grid, row, col - 1);
        explore(grid, row, col + 1);
    }
}
```

### Time/Space Complexity

- Time Complexity: O(rows * cols)
- Space Complexity: O(1)
