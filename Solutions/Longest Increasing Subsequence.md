### Algorithm

1. Create an array.
    - Keep this array sorted, with values iteratively populated by our input.
    - The length of this array will represent our solution: the length of the Longest Increasing Subsequence (LIS).
1. Progress linearly through our input.
    - For each input value, use binary search to insert it into our sorted array.
    - When inserting, we always overwrite a larger value in our sortedArray. If no such value exists, we insert at end of array.

### Example

- Input: [0, 8, 4, 12, 2]
- sortedArray: [0]
- sortedArray: [0, 8]
- sortedArray: [0, 4]
- sortedArray: [0, 4, 12]
- sortedArray: [0, 2, 12]

### Solution

```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        int[] sortedArray = new int[nums.length];
        int size = 0;
        for (int num : nums) {
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
- Time Complexity: O(n log n), since we do O(log n) binary search 'n' times
- Space Complexity: O(n)

### References

1. [Leetcode's official solution "Approach 4: Dynamic Programming with Binary Search"](https://leetcode.com/problems/longest-increasing-subsequence/solution/) - Explanation was confusing, but example and code made sense
1. [Discussion Solution](https://leetcode.com/problems/longest-increasing-subsequence/discuss/74824) - got code from here
