### Tips

- Trick: Endpoints of array give us valuable information. We apply a modified binary search to this problem.
- Although binary search compares the "middle value" to the "target value", we will break up the cases differently. We will compare middle value `A[mid]` to the start value `A[lo]`
- Array can only have 1 inflection point, therefore it is either to the left or right of `mid`. That means 1/2 of the array is ordered normally (in increasing order) and the other half has the inflection point.

### Assumptions

- Code assumes input array is:
    1. Not null
    1. Sorted then optionally rotated
    1. Without duplicate integers.

### Solution

```java
public class Solution {
    public int search(int[] A, int target) {
        int lo = 0;
        int hi = A.length - 1;
        while (lo <= hi) {
            int mid = (lo + hi) / 2;
            if (A[mid] == target) {
               return mid;
            }
            if (A[lo] < A[mid]) { // in this case, left side CANNOT have inflection point, and is increasing.
                if (A[lo] <= target && target < A[mid]) {
                    hi = mid - 1;
                } else {
                    lo = mid + 1;
                }
            } else if (A[lo] > A[mid]) {
                if (A[mid] < target && target <= A[hi]) {
                    lo = mid + 1;
                } else {
                    hi = mid - 1;
                }
            } else { // since no duplicates in input. Only happens when array is size <=2, so (lo == mid).
                lo = mid + 1; // search right, since A[lo] was already compared to 'target'.
            }
        }
        return -1;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(log n) since no duplicates exist in array
- Space Complexity: O(1)
