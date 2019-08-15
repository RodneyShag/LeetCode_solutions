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

    private void fill(int[][] image, int r, int c, int newColor, int firstColor) {
        if (r < 0 || r >= image.length || c < 0 || c >= image[0].length) {
            return;
        }
        if (image[r][c] == firstColor) {
            image[r][c] = newColor;
            fill(image, r - 1, c, newColor, firstColor);
            fill(image, r + 1, c, newColor, firstColor);
            fill(image, r, c - 1, newColor, firstColor);
            fill(image, r, c + 1, newColor, firstColor);
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols) due to recursion
