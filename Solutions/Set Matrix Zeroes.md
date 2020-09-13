# Solution

### Algorithm

1. Create a boolean array to save which rows have 0s.
1. Repeat above step for columns.
1. Loop through 2-d grid to figure out which rows & columns have a 0.
1. Re-loop through 2-d grid and set whichever entries are necessary to 0.

### Code

```java
class Solution {
    public void setZeroes(int[][] grid) {
        int M = grid.length;
        int N = grid[0].length;

        // Loop through 2-d grid to figure out which rows & columns have a 0
        boolean[] rows = new boolean[M];
        boolean[] cols = new boolean[N];
        for (int r = 0; r < M; r++) {
            for (int c = 0; c < N; c++) {
                if (grid[r][c] == 0) {
                    rows[r] = true;
                    cols[c] = true;
                }
            }
        }

        // Re-loop through 2-d grid and set whichever entries are necessary to 0
        for (int r = 0; r < M; r++) {
            for (int c = 0; c < N; c++) {
                if (rows[r] == true || cols[c] == true) {
                    grid[r][c] = 0;
                }
            }
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(rows * cols)
- Space Complexity: O(rows + cols)


# Follow-up Solution

To achieve an O(1) space solution, instead of using 2 new boolean arrays as in above solution, we will use the array itself as storage. Specifically, we will use the 0th row and 0th column as our 2 arrays. To be able to overwrite the values in the 0th row and 0th col, we will process them first.

### Algorithm

1. Check if row 0 has a 0. Save this info for later.
1. Check if col 0 has a 0. Save this info for later.
1. Use row 0 and col 0 as storage. Loop through grid and save which rows and columns have 0s.
1. Zero out the necessary cells in grid (except for 0th row and 0th col).
1. Zero out the necessary cells in row 0.
1. Zero out the necessary cells in col 0.

### Code

```java
class Solution {
    public void setZeroes(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;

        // Check if row 0 has a 0. Save this info for later.
        boolean row0Has0 = false;
        for (int c = 0; c < cols; c++) {
            if (grid[0][c] == 0) {
                row0Has0 = true;
            }
        }

        // Check if col 0 has a 0. Save this info for later.
        boolean col0Has0 = false;
        for (int r = 0; r < rows; r++) {
            if (grid[r][0] == 0) {
                col0Has0 = true;
            }
        }

        // Use row 0 and col 0 as storage.
        // Loop through grid and save which rows and columns have 0s.
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (grid[r][c] == 0) {
                    grid[r][0] = 0;
                    grid[0][c] = 0;
                }
            }
        }

        // Zero out the necessary cells in grid (except for 0th row and 0th col).
        for (int r = 1; r < rows; r++) {
            for (int c = 1; c < cols; c++) {
                if (grid[r][0] == 0 || grid[0][c] == 0) {
                    grid[r][c] = 0;
                }
            }
        }

        // Zero out the necessary cells in row 0.
        if (row0Has0) {
            for (int c = 0; c < cols; c++) {
                grid[0][c] = 0;
            }
        }

        // Zero out the necessary cells in col 0.
        if (col0Has0) {
            for (int r = 0; r < rows; r++) {
                grid[r][0] = 0;
            }
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(rows * cols)
- Space Complexity: O(1)


# Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
