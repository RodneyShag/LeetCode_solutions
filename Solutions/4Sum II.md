### Assumptions

- Integer overflow cannot occur. Problem Description says: All integers are in the range of -2<sup>28</sup> to 2<sup>28 - 1</sup> and the result is guaranteed to be at most 2<sup>31 - 1</sup>.

### Algorithm

1. Rewrite the equation as A[i] + B[j] = -(C[k] + D[l]).
1. Create a Map<Integer, Integer> where 'key' is A[i] + B[j] and 'value' is the number of pairs with this sum.
1. For each -(C[k] + D[l]), see if this desired sum is in our map. If so, add the map's 'value' to our total count.

### Solution

```java
class Solution {
    public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
        if (A == null || B == null || C == null || D == null) {
            return 0;
        }
        int count = 0;
        Map<Integer, Integer> map = new HashMap();
        for (int i = 0; i < A.length; i++) {
            for (int j = 0; j < B.length; j++) {
                map.merge(A[i] + B[j], 1, Integer::sum);
            }
        }

        for (int k = 0; k < C.length; k++) {
            for (int l = 0; l < D.length; l++) {
                int desiredSum = -(C[k] + D[l]);
                if (map.containsKey(desiredSum)) {
                    count += map.get(desiredSum);
                }
            }
        }
        return count;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(n<sup>2</sup>) since our `Map` will have n<sup>2</sup> keys if every sum A[i] + B[j] is unique

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
