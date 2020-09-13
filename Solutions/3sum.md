### Algorithm

1. Sort provided array.
1. Loop through initial array. On each i-th value, search for pairs of j, k that create a triplet summing to 0.

### Assumption

We assume integer overflow is not possible when summing any 3 numbers in `int[] num`.

### Solution

```java
class Solution {
    public List<List<Integer>> threeSum(int[] num) {
        List<List<Integer>> result = new ArrayList();
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

### Time Complexity

O(n<sup>2</sup>)

### Space Complexity

- O(n<sup>2</sup>) due to the line `result.add(Arrays.asList(num[i], num[j], num[k]))`.
- Example runs
  - `[-10, -9, -8, -7, -6, -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]` has 50 solutions
  - `[-20, -19, -18, -17, -16, -15, -14, -13, -12, -11, -10, -9, -8, -7, -6, -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]` has 200 solutions
  - Having the input array be approximately 2 times the size did not double the number of solutions. It increased the number of solutions by a factor of 2<sup>2</sup> = 4. This hints that the space complexity is indeed O(n<sup>2</sup>)
- This [StackOverflow comment](https://stackoverflow.com/a/57641288) attempts to prove that the solution set is of size O(n<sup>2</sup>)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
