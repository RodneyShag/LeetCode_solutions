### Hint

Copy to end of array since that's where our empty buffer is.

### Solution

```java
class Solution {
    public void merge(int[] A, int m, int[] B, int n) {
        int lastA = m - 1;
        int lastB = n - 1;
        int curr = lastA + lastB + 1;
        while (lastA >= 0 && lastB >= 0) {
            if (A[lastA] > B[lastB]) {
                A[curr--] = A[lastA--];
            } else {
                A[curr--] = B[lastB--];
            }
        }

        // Copy Remaining Elements. No need to copy lastA elements since they're already in correct spot
        while (lastB >= 0) {
            A[curr--] = B[lastB--];
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
