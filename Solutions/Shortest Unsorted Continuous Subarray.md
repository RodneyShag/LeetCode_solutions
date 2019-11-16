### Algorithm

- Find these 2 indices
  - `endIndex`: index that, if we sort from 0 to endIndex, entire array is sorted
  - `startIndex`: index that, if we sort from startIndex to end, entire array is sorted
- Sorting from `startIndex` to `endIndex` will make the entire array sorted

### Solution

```java
class Solution {
    public int findUnsortedSubarray(int[] array) {
        if (array == null || array.length == 0) {
            return 0;
        }

        int startIndex = -1;
        int endIndex   = -1;

        // find endIndex
        int maxSoFar = array[0];
        for (int i = 0; i < array.length; i++) {
            if (array[i] < maxSoFar) {
                endIndex = i;
            }
            maxSoFar = Math.max(maxSoFar, array[i]);
        }

        // find startIndex
        int minSoFar = array[array.length - 1];
        for (int i = array.length - 1; i >= 0; i--) {
            if (array[i] > minSoFar) {
                startIndex = i;
            }
            minSoFar = Math.min(minSoFar, array[i]);
        }

        if (startIndex == -1 || endIndex == -1) {
            return 0;
        }
        return endIndex - startIndex + 1;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/discuss/323450)
- [github.com/RodneyShag](https://github.com/RodneyShag)
