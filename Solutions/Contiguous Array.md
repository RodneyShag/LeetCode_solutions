### Algorithm

1. Create "deltas" array. Each value in this array will represent (number of 1s) minus (number of 0s) seen so far.
1. Create a HashMap<Integer, Integer>, that for each delta, it saves the first index we saw this delta in our array
    - "key" is the "delta" calculated earlier
    - "value" is first index of this delta in original array

### Example

```
 index: [ 0  1  2  3  4  5  6  7]
 input: [ 0  0  1  0  0  0  1  1]
deltas: [-1 -2 -1 -2 -3 -4 -3 -2]
```

- In `int[] deltas`, if 2 indices have the same value, then number of 0s and number of 1s are equal between these indices.
- The largest valid subarray corresponds to the largest `j-i` where `deltas[i] == deltas[j]`.
- In this case, `i=1`, `j=7`, `deltas[i] == deltas[j] == -2`, and `j-i = 7-1 = 6`.
- This corresponds to subarray `(i, j]` which is `[1, 0, 0, 0, 1, 1]`

### Solution

```java
class Solution {
    private int[] findDeltas(int[] array) {
        int[] deltas = new int[array.length];
        int delta = 0;
        for (int i = 0; i < array.length; i++) {
            if (array[i] == 1) {
                delta++;
            } else if (array[i] == 0) {
                delta--;
            }
            deltas[i] = delta;
        }
        return deltas;
    }

    public int findMaxLength(int[] array) {
        if (array == null) {
            return 0;
        }
        int[] deltas = findDeltas(array);
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1); // for testcases such as [1, 0], [1, 0, 0]
        int maxLength = 0;
        for (int i = 0; i < array.length; i++) {
            if (!map.containsKey(deltas[i])) {
                map.put(deltas[i], i);
            } else {
                maxLength = Math.max(maxLength, i - map.get(deltas[i]));
            }
        }
        return maxLength;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)
