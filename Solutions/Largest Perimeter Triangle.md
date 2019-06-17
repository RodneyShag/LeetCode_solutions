### Algorithm

For a triangle to have non-zero area, the 2 shorter sides must sum to be larger than the larger side.

1. Sort the array - the larger numbers will be at the end of the array
1. Grab triplets in decreasing order of size (right-to-left in array) and see if they form a valid triangle

### Solution

```java
class Solution {
    public int largestPerimeter(int[] A) {
        Arrays.sort(A);
        for (int i = A.length - 1; i >= 2; i--) {
            if (A[i - 2] + A[i - 1] > A[i]) {
                return A[i - 2] + A[i - 1] + A[i];
            }
        }
        return 0;
    }
}
```

### Time/Space Complexity

- Time Complexity: `O(n log n)` due to Arrays.sort()
- Space Complexity: `O(n)` due to loop
