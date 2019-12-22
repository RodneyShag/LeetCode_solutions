### Algorithm + Example

Solve [LeetCode #461 - Hamming Distance](https://leetcode.com/problems/hamming-distance) first before solving this problem. [Here is that problem's solution](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Hamming%20Distance.md).

If there are `n` integers in the array and `k` of them have a particular bit set and `n-k` do not, then that bit contributes `k * (n - k)` hamming distance to the total.

```
a = 0 1 0
b = 0 1 1
c = 0 0 1
d = 0 1 0
e = 1 1 0
        ↑
```

- Let's calculate the Hamming Distance for the last digit of all the numbers
- There are 5 numbers above. For the last digit, we have 3 ones and 2 zeros
- This gives us `total hamming distance = ones * zeros = 3 * 2 = 6`. Let's doublecheck this by examining every pair we can make using the last digits in the numbers:

```
(0, 0) (0, 1) (0, 0) (0, 0)
(1, 1) (1, 0) (1, 0)
(1, 0) (1, 0)
(0, 0)
```

Notice only 6 of the above 10 pairs have both a `0` and a `1`, so only 6 of them contribute to the hamming distance.

To get the total hamming distance, use this idea on all 32 digits, which is the size of a Java `int`

### Solution

```java
class Solution {
    public int totalHammingDistance(int[] nums) {
        if (nums == null) {
            return 0;
        }
        int total = 0;
        for (int i = 0; i < 32; i++) {
            int ones = 0;
            for (int j = 0; j < nums.length; j++) {
                ones += (nums[j] >> i) & 1;
            }
            total += ones * (nums.length - ones);
        }
        return total;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/total-hamming-distance/discuss/457802)
- [github.com/RodneyShag](https://github.com/RodneyShag)
