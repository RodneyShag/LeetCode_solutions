### Algorithm

1. Preprocess the data: create 2 additional matrices.
    - In `left[][]`, for each cell, we store the number of ones immediately at left (and itself)
    - In   `up[][]`, for each cell, we store the number of ones immediately above (and itself)

```
grid[3][3] = 1 1 1    left[3][3] = 1 2 3    up[3][3] = 1 1 1
             1 0 1                 1 0 1               2 0 2
             1 1 1                 1 2 3               3 1 3
```
2. Search for largest squares first. Loop through our `grid`. Treat each cell as a top-left corner of a square, and check if a valid square can be made from there.

### Solution

```java
class Solution {
    public int largest1BorderedSquare(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;

        int[][] left = new int[rows][cols];
        int[][]   up = new int[rows][cols];

        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (grid[r][c] == 1) {
                    left[r][c] = (c == 0) ? 1 : left[r][c - 1] + 1;
                      up[r][c] = (r == 0) ? 1 :   up[r - 1][c] + 1;
                }
            }
        }

        for (int side = Math.min(rows, cols); side > 0; side--) {
            for (int r = 0; r + side - 1 < rows; r++) {
                for (int c = 0; c + side - 1 < cols; c++) {
                    if (left[r][c + side - 1] >= side
                    && left[r + side - 1][c + side - 1] >= side
                    && up[r + side - 1][c] >= side
                    && up[r + side - 1][c + side - 1] >= side) {
                        return side * side;
                    }
                }
            }
        }
        return 0;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>3</sup>) due to 3 nested "for" loops
- Space Complexity: O(n<sup>2</sup>) due to preprocessing

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/largest-1-bordered-square/discuss/360612)
- [github.com/RodneyShag](https://github.com/RodneyShag)
