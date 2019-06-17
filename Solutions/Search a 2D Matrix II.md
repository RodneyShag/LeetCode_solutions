### Algorithm

- On every step, eliminate a row or a column.
  - Start in top right corner (since the numbers below it are bigger, and numbers to left are smaller)
  - Always either move down (eliminating current row), or move left (eliminating current col)

### Solution

```java
class Solution {
    public boolean searchMatrix(int[][] grid, int target) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return false;
        }
        int rows = grid.length;
        int cols = grid[0].length;

        // Start at top right corner
        int row = 0;
        int col = cols - 1;

        while (row < rows && col >= 0) {
            if (grid[row][col] == target) {
                return true;
            } else if (grid[row][col] > target) {
                col--;
            } else {
                row++;
            }
        }
        return false;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(rows * cols)
- Space Complexity: O(1)

### Alternative Solution 1

Instead of starting from top-right and moving to bottom-left, do it the other way around: start from bottom-left and move to top-right.

### Alternative Solution 2

Binary search every row. However, this solution is slower, as it's for O(rows * log(cols)) runtime.
