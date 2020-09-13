### Algorithm

1. Sort provided array.
1. Loop through initial array. On each i-th value, search for pairs of j, k that create a triplet with a sum closest to our "target".

### Assumption

We assume integer overflow is not possible when summing any 3 numbers in `int[] num`.

### Solution

```java
class Solution {
    public int threeSumClosest(int[] num, int target) {
        if (num == null || num.length < 3) {
            return Integer.MAX_VALUE; // no solution
        }
        Arrays.sort(num);
        int bestSum = num[0] + num[1] + num[2];
        for (int i = 0; i < num.length - 2; i++) {
            int j = i + 1;
            int k = num.length - 1;
            while (j < k) {
                int sum = num[i] + num[j] + num[k];
                if (Math.abs(sum - target) < Math.abs(bestSum - target)) {
                    bestSum = sum;
                }
                if (sum < target) {
                    j++;
                } else if (sum > target) {
                    k--;
                } else {
                    return target; // we found an exact match
                }
            }
        }
        return bestSum;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: Depends on `Arrays.sort()`. Can be as low as O(1).

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
