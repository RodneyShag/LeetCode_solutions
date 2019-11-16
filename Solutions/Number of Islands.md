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

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/number-of-islands/discuss/304470)
- [github.com/RodneyShag](https://github.com/RodneyShag)
