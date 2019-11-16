### Algorithm

Use Gauss's formula: The sum of 1 to n is (n)(n+1)/2

### Solution

```java
class Solution {
    public int missingNumber(int[] nums) {
        int expectedSum = nums.length * (nums.length + 1) / 2;
        int actualSum = 0;
        for (int num : nums) {
            actualSum += num;
        }
        return expectedSum - actualSum;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/missing-number/discuss/304380)
- [github.com/RodneyShag](https://github.com/RodneyShag)
