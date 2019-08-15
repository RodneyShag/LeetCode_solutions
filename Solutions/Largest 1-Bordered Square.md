### Solution

```java
class Cell { // public variables for simplicity
    int onesRight = 0; // including itself
    int onesDown  = 0; // including itself

    public Cell(int right, int down) {
        onesRight = right;
        onesDown  = down;
    }
}

class Subsquare { // public variables for simplicity
    int row;
    int col;
    int length;

    public Subsquare(int r, int c, int l) {
        row    = r;
        col    = c;
        length = l;
    }
}

class Solution {
    int rows;
    int cols;

    private Cell[][] preprocessGrid(int[][] grid) { // O(n^2)
        rows = grid.length;
        cols = grid[0].length;

        Cell[][] preprocessed = new Cell[rows][cols];
        for (int r = rows - 1; r >= 0; r--) {
            for (int c = cols - 1; c >= 0; c--) {
                preprocessed[r][c] = new Cell(0, 0);
                if (grid[r][c] == 1) {
                    preprocessed[r][c].onesRight = 1 + ((c + 1 < cols) ? preprocessed[r][c + 1].onesRight : 0);
                    preprocessed[r][c].onesDown  = 1 + ((r + 1 < rows) ? preprocessed[r + 1][c].onesDown  : 0);
                }
            }
        }
        return preprocessed;
    }

    public int largest1BorderedSquare(int[][] grid) {
        Subsquare ss = findLargestSubsquare(grid);
        return ss == null ? 0 : ss.length * ss.length;
    }

    private Subsquare findLargestSubsquare(int[][] grid) { // O(n) * runtime of findSubSquare()
        Cell[][] processed = preprocessGrid(grid);
        for (int dimension = Math.min(rows, cols); dimension >= 1; dimension--) {
            Subsquare ss = findSubsquare(processed, dimension);
            if (ss != null) {
                return ss;
            }
        }
        return null;
    }

    private Subsquare findSubsquare(Cell[][] cellMatrix, int length) { // O(n^2) (since 2 for loops)
        int wiggleRoomRows = rows - length;
        int wiggleRoomCols = cols - length;

        for (int r = 0; r <= wiggleRoomRows; r++) {
            for (int c = 0; c <= wiggleRoomCols; c++) {
                if (isValidSquare(cellMatrix, r, c, length)) {
                    return new Subsquare(r, c, length);
                }
            }
        }
        return null;
    }

    // r, c represent top-left corner of square
    private boolean isValidSquare(Cell[][] cellMatrix, int r, int c, int length) { // O(1)
        if (r + length - 1 >= rows || c + length - 1 >= cols) {
            return false;
        }
        Cell topLeft     = cellMatrix[r][c];
        Cell topRight    = cellMatrix[r][c + length - 1];
        Cell bottomLeft  = cellMatrix[r + length - 1][c];
        Cell bottomRight = cellMatrix[r + length - 1][c + length - 1];
        if (topLeft.onesDown < length || topLeft.onesRight < length) {
            return false;
        } else if (topRight.onesDown < length || topRight.onesRight < 1) {
            return false;
        } else if (bottomLeft.onesDown < 1 || bottomLeft.onesRight < length) {
            return false;
        } else if (bottomRight.onesDown < 1 || bottomRight.onesRight < 1) {
            return false;
        }
        return true;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>3</sup>)
- Space Complexity: O(n<sup>2</sup>)
