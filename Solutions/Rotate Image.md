### Algorithm

1. Transpose the image
1. Flip the image horizontally (along a vertical line down middle of image)

Example:

```
Original   Tranposed    Flipped
 1 2 3       1 4 7       7 4 1
 4 5 6  -->  2 5 8  -->  8 5 2
 7 8 9       3 6 9       9 6 3
```

### Solution

```java
class Solution {
    private int n;

    public void rotate(int[][] image) {
        if (image == null || image.length != image[0].length) {
            return;
        }
        n = image.length;
        transpose(image);
        flipHorizontally(image);
    }

    private void transpose(int[][] image) {
        for (int row = 0; row < n; row++) {
            for (int col = row + 1; col < n; col++) {
                swap(image, row, col, col, row);
            }
        }
    }

    private void flipHorizontally(int[][] image) {
        for (int row = 0; row < n; row++) {
            for (int col = 0; col < n / 2; col++) {
                swap(image, row, col, row, n - 1 - col);
            }
        }
    }

    private void swap(int[][] image, int r1, int c1, int r2, int c2) {
        int temp      = image[r1][c1];
        image[r1][c1] = image[r2][c2];
        image[r2][c2] = temp;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/rotate-image/discuss/304523)
- [github.com/RodneyShag](https://github.com/RodneyShag)
