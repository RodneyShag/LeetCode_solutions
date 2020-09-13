### Algorithm

- Since we're asked for a range, we can use [binary search](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Binary%20Search.md) 2 times.
- Create 2 variations of binary search: 1 for the left endpoint of the range, and 1 for the right endpoint.
- Optimization: once we found the left endpoint, we don't need to search the entire array for the right endpoint. We will use the left endpoint as a lower bound to `findLast()`

### Solution

```java
class Solution {
    public int[] searchRange(int[] A, int target) {
        if (A == null || A.length == 0) {
            return new int[]{-1, -1};
        }
        int[] result = new int[2];
        result[0] = findFirst(A, target);
        if (result[0] == -1) {
            return new int[]{-1, -1};
        }
        result[1] = findLast(A, target, result[0]);
        return result;
    }

    private int findFirst(int[] A, int target) {
        int lo = 0;
        int hi = A.length - 1;
        while (lo < hi) {
            int mid = (lo + hi) / 2; // bias towards left
            if (A[mid] < target) {
                lo = mid + 1;
            } else if (A[mid] > target) {
                hi = mid - 1;
            } else {
                hi = mid; // bias towards left
            }
        }
        return A[lo] == target ? lo : -1;
    }

    private int findLast(int[] A, int target, int lo) {
        int hi = A.length - 1;
        while (lo < hi) {
            int mid = (lo + hi) / 2 + 1; // bias towards right
            if (A[mid] < target) {
                lo = mid + 1;
            } else if (A[mid] > target) {
                hi = mid - 1;
            } else {
                lo = mid; // bias towards right
            }
        }
        return A[hi] == target ? hi : -1;
    }
}
```


### Example

- `findFirst()` using `mid = (lo + hi) / 2`
- Search array for 4

```
[3,  4,  4,  4,  5,  5,  5]
 lo                     hi
            mid

[3,  4,  4,  4,  5,  5,  5]
 lo          hi
    mid

[3,  4,  4,  4,  5,  5,  5]
 lo  hi
mid

[3,  4,  4,  4,  5,  5,  5]
     lo
     hi
    mid

Loop ends. Index 1 is returned.
```

- `findLast()` using `mid = (lo + hi) / 2 + 1`
- Search array for 4

```

[3,  4,  4,  4,  5,  5,  5]
 lo                     hi
            mid

[3,  4,  4,  4,  5,  5,  5]
            lo          hi
                    mid

[3,  4,  4,  4,  5,  5,  5]
             lo  hi
                mid

[3,  4,  4,  4,  5,  5,  5]
            lo
            hi
            mid

Loop ends. Index 3 is returned.
```


### Implementation Details

- Having 2 separate functions for binary search results in more code, but makes the code easier to follow.
- The differences between the above functions and [binary search](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Binary%20Search.md) are
    1. When `A[mid] == target`, instead of returning mid, we either do `hi = mid` to bias left, or `lo = mid` to bias right
    1. We use `mid = (lo + hi) / 2` to bias left and `mid = (lo + hi) / 2 + 1` to bias right
        - This is useful for 2-element arrays
    1. We loop while `lo < hi` instead of `lo <= hi`
        - This is useful for 1-element arrays. The loop ends and we check for a match

### Time/Space Complexity

-  Time Complexity: `O(log n)`
- Space Complexity: `O(1)`

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
