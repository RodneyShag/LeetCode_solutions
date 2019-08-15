### Algorithm

1. Use Dynamic Programming. For each element in array, save the sum from beginning of array until that element.
    - key: sum
    - value: number of contiguous arrays, starting at beginning of array, that sum to "key: sum"
1. Our `HashMap` tells us `SUM[0...i]`. Our current `sum` gives us `SUM[0...j]`. So subtraction gives us `SUM[0...j] - SUM[0...i] = SUM(i...j]` (the parenthesis is there since `i` is not included in that range). Each `SUM(i...j] == k` gives us 1 solution.

### Solution

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> savedSum = new HashMap<>();
        savedSum.put(0, 1);
        int sum = 0;
        int result = 0;        
        for (int num : nums) {
            sum += num;
            result += savedSum.getOrDefault(sum - k, 0);
            savedSum.merge(sum, 1, Integer::sum);
        }
        return result;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)
