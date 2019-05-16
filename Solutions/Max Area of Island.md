### Algorithm

- Loop through our `char[][] grid`. For each piece of land, we recursively search its neighbors to calculate island size.
- We mark land by simply changing the `1` in our `grid` to a `0`.

### Solution

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
        int rows = grid.length;
        int cols = grid[0].length;
        int maxRegion = 0;
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                // Find the largest region from the current cell
                if (grid[row][col] == 1) {
                    int size  = findLargestRegion(grid, row, col, rows, cols);
                    maxRegion = Math.max(maxRegion, size);
                }
            }
        }
        return maxRegion;
    }

    private int findLargestRegion(int[][] grid, int row, int col, int rows, int cols) {
        if (row < 0 || row >= rows || col < 0 || col >= cols || grid == null || grid[row][col] == 0) {
            return 0;
        }

        grid[row][col] = 0; // we alter the original matrix here
        int size = 1;

        // Recursively search neighbors
        size += findLargestRegion(grid, row - 1, col, rows, cols);
        size += findLargestRegion(grid, row + 1, col, rows, cols);
        size += findLargestRegion(grid, row, col - 1, rows, cols);
        size += findLargestRegion(grid, row, col + 1, rows, cols);

        return size;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols)
