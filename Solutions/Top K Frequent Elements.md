### Algorithm

1. Create HashMap of number frequencies. Frequency = # of times a number appears in array.
1. Create buckets, 1 for each possible frequency. Fill buckets with numbers from input, based on their frequency.
1. To get the most frequent elements, loop through the buckets in descending order.

### Solution

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return Collections.<Integer>emptyList();
        }

        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.merge(num, 1, Integer::sum);
        }

        List<List<Integer>> buckets = new ArrayList<>(nums.length + 1); // wont use 0th bucket
        for (int i = 0; i < nums.length + 1; i++) {
            buckets.add(new ArrayList<Integer>());
        }

        for (Integer num : map.keySet()) {
            int frequency = map.get(num);
            List<Integer> bucket = buckets.get(frequency);
            bucket.add(num);
        }

        List<Integer> solution = new ArrayList<>();
        for (int i = buckets.size() - 1; i >= 0 && solution.size() < k; i--) {
            List<Integer> bucket = buckets.get(i);
            solution.addAll(bucket);
        }
        return solution;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/top-k-frequent-elements/discuss/304390)
- [github.com/RodneyShag](https://github.com/RodneyShag)
