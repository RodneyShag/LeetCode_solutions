### Algorithm

Rotate array (in place) using 3 reverse operations

### Solution

```java
class Solution {
    public void rotate(int[] nums, int k) {
        if (nums == null) {
            return;
        }
        k %= nums.length; // to account for k > length of array
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }

    private void reverse(int[] array, int start, int end) {
        if (array == null || start < 0 || start >= array.length || end < 0 || end >= array.length) {
            return;
        }
        while (start < end) {
            swap(array, start++, end--);
        }
    }

    private void swap(int[] array, int i, int j) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1) by doing an "in place" rotation
