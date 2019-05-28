### Algorithm

[Tutorial video](https://www.youtube.com/watch?v=LPFhl65R7ww)

### Solution

`findMedianSortedArrays()` below assumes input arrays are sorted.

```java
class Solution {
    public double findMedianSortedArrays(int[] input1, int[] input2) throws IllegalArgumentException {
        if (input1 == null || input2 == null) {
            throw new IllegalArgumentException();
        } else if (input1.length > input2.length) {
            return findMedianSortedArrays(input2, input1); // ensures 1st array is smaller than 2nd array
        }
        int x = input1.length;
        int y = input2.length;

        int low = 0;
        int high = x;
        while (low <= high) {
            int partitionX = (low + high) / 2;
            int partitionY = (x + y + 1) / 2 - partitionX;

            int maxLeftX  = (partitionX == 0) ? Integer.MIN_VALUE : input1[partitionX - 1];
            int minRightX = (partitionX == x) ? Integer.MAX_VALUE : input1[partitionX];

            int maxLeftY  = (partitionY == 0) ? Integer.MIN_VALUE : input2[partitionY - 1];
            int minRightY = (partitionY == y) ? Integer.MAX_VALUE : input2[partitionY];

            if (maxLeftX <= minRightY && maxLeftY <= minRightX) {
                if ((x + y) % 2 == 0) {
                    return ((double) Math.max(maxLeftX, maxLeftY) + Math.min(minRightX, minRightY)) / 2;
                } else {
                    return (double) Math.max(maxLeftX, maxLeftY);
                }
            } else if (maxLeftX > minRightY) {
                high = partitionX - 1;
            } else {
                low = partitionX + 1;
            }
        }

        throw new IllegalArgumentException(); // can only occur if input arrays were not sorted.
    }
}      
```

### Time/Space Complexity

- Time Complexity: O(min(log(x, y)))
- Space Complexity: O(1)
