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
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                // Find the largest region from the current cell
                if (grid[r][c] == 1) {
                    int size  = findLargestRegion(grid, r, c, rows, cols);
                    maxRegion = Math.max(maxRegion, size);
                }
            }
        }
        return maxRegion;
    }

    private int findLargestRegion(int[][] grid, int r, int c, int rows, int cols) {
        if (r < 0 || r >= rows || c < 0 || c >= cols || grid == null || grid[r][c] == 0) {
            return 0;
        }

        grid[r][c] = 0; // we alter the original matrix here
        int size = 1;

        // Recursively search neighbors
        size += findLargestRegion(grid, r - 1, c, rows, cols);
        size += findLargestRegion(grid, r + 1, c, rows, cols);
        size += findLargestRegion(grid, r, c - 1, rows, cols);
        size += findLargestRegion(grid, r, c + 1, rows, cols);

        return size;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
