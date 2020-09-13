### Solution

```java
class Solution {
    public int search(int[] sortedArray, int value) {
        int lo = 0;
        int hi = sortedArray.length - 1;

        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
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

### Implementation Details

Instead of calculating the middle value as `mid = (lo + hi) / 2`, do `mid = lo + (hi - lo) / 2` to avoid integer overflow

### Time/Space Complexity

- Time Complexity: O(log n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
