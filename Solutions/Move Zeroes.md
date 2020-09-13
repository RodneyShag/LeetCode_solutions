### Algorithm

1. Loop through array and write any non-zero values to beginning of array.
1. For remaining indices we didn't write to, set their values to 0.

### Solution

```java
class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }
        int i = 0;
        for (int num : nums) {
            if (num != 0) {
                nums[i] = num;
                i++;
            }
        }
        while (i < nums.length) {
            nums[i] = 0;
            i++;
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1) since we overwrite the array that was provided to us

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
