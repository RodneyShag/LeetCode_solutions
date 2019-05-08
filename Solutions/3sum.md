### Algorithm

1. Sort provided array.
1. Loop through initial array. On each i-th value, search for pairs of j, k that create a triplet summing to 0.

### Assumption

We assume integer overflow is not possible when summing any 3 numbers in `int[] num`.

### Solution

```java
class Solution {
    public List<List<Integer>> threeSum(int[] num) {
        List<List<Integer>> result = new ArrayList<>();
        if (num == null || num.length < 3) {
            return result; // no solution
        }
        Arrays.sort(num);
        for (int i = 0; i < num.length - 2; i++) {
            if (i > 0 && num[i] == num[i-1]) {
                continue; // skip duplicates
            }
            int wantedSum = 0 - num[i];
            int j = i + 1;
            int k = num.length - 1;
            while (j < k) {
                int actualSum = num[j] + num[k];
                if (actualSum == wantedSum) {
                    result.add(Arrays.asList(num[i], num[j], num[k]));
                    while (j < k && num[j] == num[j+1]) {
                        j++; // skip duplicates
                    }
                    while (j < k && num[k] == num[k-1]) {
                        k--; // skip duplicates
                    }
                    j++;
                    k--;
                } else if (actualSum < wantedSum) {
                    j++;
                } else {
                    k--;
                }
            }
        }
        return result;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: Depends on `Arrays.sort()`. Can be as low as O(1).
