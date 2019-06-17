### Algorithm

Use Depth-First Search (DFS) to fill the image.

Need to check `image[startRow][startCol] == newColor` before we start DFS, as otherwise we will be in an infinite loop.

### Solution

```java
class Solution {
    public int[][] floodFill(int[][] image, int startRow, int startCol, int newColor) {
        if (image == null || image[startRow][startCol] == newColor) {
            return image;
        }
        fill(image, startRow, startCol, newColor, image[startRow][startCol]);
        return image;
    }

    private void fill(int[][] image, int row, int col, int newColor, int firstColor) {
        if (row < 0 || row >= image.length || col < 0 || col >= image[0].length) {
            return;
        }
        if (image[row][col] == firstColor) {
            image[row][col] = newColor;
            fill(image, row - 1, col, newColor, firstColor);
            fill(image, row + 1, col, newColor, firstColor);
            fill(image, row, col - 1, newColor, firstColor);
            fill(image, row, col + 1, newColor, firstColor);
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols) due to recursion
