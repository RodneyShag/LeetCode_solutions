### Algorithm

 There is just 1 place in the array where the versions go from "good" to "bad". We can use a modified version of [binary search](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Binary%20Search.md) to find this location.

### Provided Code

`boolean isBadVersion(int version)` is defined in the parent class `VersionControl`.

### Solution

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int lo = 1;
        int hi = n;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (isBadVersion(mid)) {
                hi = mid;
            } else {
                lo = mid + 1;
            }
        }
        return hi;
    }
}
```

### Implementation Details

Instead of calculating the middle value as `mid = (lo + hi) / 2`, do `mid = lo + (hi - lo) / 2` to avoid integer overflow

### Time/Space Complexity

-  Time Complexity: O(log n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/first-bad-version/discuss/457444)
- [github.com/RodneyShag](https://github.com/RodneyShag)
