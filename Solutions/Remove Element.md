### Notes

The problem mentions "It doesn't matter what you leave beyond the new length."

### Solution

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        if (nums == null) {
            return 0;
        }
        int i = 0;
        for (int n : nums) {
            if (n != val) {
                nums[i] = n;
                i++;
            }
        }
        return i;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
