### Algorithm

This is a dynamic programming problem.

Our robot can only move down and right. So for each cell, there are 2 ways to get to it. In most cases this gives us `maze[r][c] = maze[r][c - 1] + maze[r - 1][c]`. The rest of the code accounts for edge cases:
  1. If a cell has a "1" in it
  1. Top-Left corner cell
  1. Top Row
  1. Left Column

### Solution

```java
class Solution {
    int count = 0;
    public int uniquePathsWithObstacles(int[][] maze) {
        if (maze == null || maze[0][0] == 1) {
            return 0;
        }        
        int rows = maze.length;
        int cols = maze[0].length;

        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (maze[r][c] == 1) {
                    maze[r][c] = 0;
                } else if (r == 0 && c == 0) {
                    maze[r][c] = 1;
                } else if (r == 0) {
                    maze[r][c] = maze[r][c - 1];
                } else if (c == 0) {
                    maze[r][c] = maze[r - 1][c];
                } else {
                    maze[r][c] = maze[r][c - 1] + maze[r - 1][c];
                }
            }
        }

        return maze[rows - 1][cols - 1];
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(rows * cols)
- Space Complexity: O(1), assuming we're allowed to alter the original maze

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
