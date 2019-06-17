### Solution

```java
class Solution {
    public int search(int[] sortedArray, int value) {
        int lo = 0;
        int hi = sortedArray.length - 1;

        while (lo <= hi) {
            int mid = (lo + hi) / 2;
            if (sortedArray[mid] > value) {
                hi = mid - 1;
            } else if (sortedArray[mid] < value) {
                lo = mid + 1;
            } else {
                return mid;
            }
        }
        return -1;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(log n)
- Space Complexity: O(1)
