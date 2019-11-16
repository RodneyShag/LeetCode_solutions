### Algorithm

1. Sort by increasing height, decreasing width. So if we have [width, height] of [2, 5], [2, 6], [2,7], they would be sorted to [2, 7], [2, 6], [2,5]
1. Since the widths are already in increasing order, we can use the [Longest Increasing Subsequence (LIS)](https://leetcode.com/problems/longest-increasing-subsequence/) algorithm on the heights to get our answer. [Here is an implementation of LIS](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Longest%20Increasing%20Subsequence.md)

### Example

```
[width, height] sorted by width increasing, height decreasing:
[1 2] [1 1]   [2 2]   [3 4] [3 3]   [4 4]

The heights are:
[_ 2] [_ 1]   [_ 2]   [_ 4] [_ 3]   [_ 4]

Longest Increasing Subsequence (LIS) on heights gives us:
      [_ 1]   [_ 2]         [_ 3]   [_ 4]

solution:
      [1 1]   [2 2]         [3 3]   [4 4]
```

### Solution

```java
class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        if (envelopes == null || envelopes.length == 0 || envelopes[0].length != 2) {
            return 0;
        }
        Arrays.sort(envelopes, (a, b) -> {
            if (a[0] != b[0]) {
                return a[0] - b[0];
            } else {
                return b[1] - a[1];
            }
        });

        // Longest Increasing Subsequence Algorithm
        int[] sortedArray = new int[envelopes.length];
        int size = 0;
        for (int[] envelope : envelopes) {
            int num = envelope[1];
            int start = 0;
            int end = size; // 1 element past end of our sortedArray
            while (start != end) {
                int mid = (start + end) / 2;
                if (sortedArray[mid] < num) {
                    start = mid + 1;
                } else {
                    end = mid;
                }
            }
            sortedArray[start] = num;
            if (start == size) {
                size++;
            }
        }
        return size;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n log n) due to sorting
- Space Complexity: O(n) for storing `sortedArray` variable

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/russian-doll-envelopes/discuss/348428)
- [github.com/RodneyShag](https://github.com/RodneyShag)
