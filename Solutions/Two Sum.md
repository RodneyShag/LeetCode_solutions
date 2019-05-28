### Solution

```java
class Solution {    
    public int[] twoSum(int[] array, int target) throws IllegalArgumentException {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < array.length; i++) {
            int complement = target - array[i];
            if (map.containsKey(complement)) {
                return new int[]{ map.get(complement), i };
            }
            map.put(array[i], i);
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)
