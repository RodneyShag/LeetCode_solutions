### Algorithm

1. We are given an array of numbers. Given an index, this array returns a number in O(1) time.
1. However, we want something different. We would rather have a data structure that, when provided a _value_, gives us the _index_ in O(1) time. `HashMap` to the rescue!
1. Create a `HashMap`. As we loop through the array, populate the `HashMap` with each number, where the `HashMap` "key" is the number, and the `HashMap` "value" is the index of the number in the array.
1. For each number, we check our `HashMap` to see if the complement exists in it. If so, we've found a pair of numbers that create our solution.

Implementation Detail: First check the `HashMap` for the complement before putting the current number in it.

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
