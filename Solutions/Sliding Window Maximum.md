### Algorithm

1. Represent the sliding window using a `Deque<Integer>`.
    - Instead of storing values, the `Deque` will store __indices__ of the elements in the array. This simplifies discarding elements in the next step.
1. Before adding a new element to the `Deque`, we
    - discard index if it's no longer in the sliding window
    - Remove indices that can no longer represent a max.
1. The head of the `Deque` will always be an index `i` where `A[i]` is the maximum in the corresponding "sliding window".
    - Notice the indices in `Deque` will always be increasing, representing values from the array that will always be decreasing

### Solution

```java
class Solution {
    public int[] maxSlidingWindow(int[] A, int k) {
        if (A == null || A.length == 0 || k < 0 || k > A.length) {
            return A;
        }
        Deque<Integer> deque = new ArrayDeque();
        int[] result = new int[A.length - k + 1];
        for (int i = 0; i < A.length; i++) {
            // discard element if it's no longer in the sliding window
            if (!deque.isEmpty() && deque.peek() <= i - k) {
                deque.removeFirst();
            }
            // Remove elements that could no longer be a max
            while (!deque.isEmpty() && A[i] >= A[deque.peekLast()]) {
                deque.removeLast();
            }

            deque.addLast(i);

            if (i - k + 1 >= 0) {
                result[i - k + 1] = A[deque.peek()];
            }
        }
        return result;
    }
}
```

### Example

```
Input:
  nums = [1 3 -1 -3 5 3 6 7]
  k = 3

Window position                Max      Deque (storing indices)
---------------               -----     -----
[1]  3  -1 -3  5  3  6  7       -       [0]
[1  3]  -1 -3  5  3  6  7       -       [1]
[1  3  -1] -3  5  3  6  7       3       [1 2]
 1 [3  -1  -3] 5  3  6  7       3       [1 2 3]
 1  3 [-1  -3  5] 3  6  7       5       [4]
 1  3  -1 [-3  5  3] 6  7       5       [4 5]
 1  3  -1  -3 [5  3  6] 7       6       [6]
 1  3  -1  -3  5 [3  6  7]      7       [7]

Output: [3 3 5 5 6 7]
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
