### Algorithm

__Similar problem__ to [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/). Review [my solution to that problem](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Find%20Median%20from%20Data%20Stream.md) first, as we will be use the same algorithm explained there.

__Heap vs. TreeSet__ - removing a specific element from a heap takes `O(k)` time. Instead, use a [TreeSet](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html) to achieve `O(log k)` for removal. Also, iterating over a `TreeSet` returns the elements in sorted order, so grabbing the largest or smallest element in a `TreeSet` takes `O(1)` time (which also means we don't need to `reverse()` our `Comparator` like we did in the previous problem)

__Dealing with duplicate values in input array__ - Normally we would store _values_ in our `TreeSet`, but since duplicate values can exist, we will store _indexes_ instead, which are unique. Using an index, we can always retrieve the corresponding value using the input array.

__Comparator for TreeSet__ - Our comparator will take 2 indices and compare their _corresponding values in the input array_. In the edge case where the values are equal, we compare the indexes instead. This last step of comparing indexes is required since otherwise, the 2 elements in the `TreeSet` would be equivalent and thus 1 of them would be removed (since a `TreeSet` is an `AbstractSet` which removes duplicates)


### Solution

```java
class Solution {
    public double[] medianSlidingWindow(int[] nums, int k) {
        if (nums == null || k == 0 || k > nums.length) {
            return new double[0];
        }
        Comparator<Integer> comparator = (a, b) -> nums[a] != nums[b]
                                                 ? Integer.compare(nums[a], nums[b])
                                                 : a - b;
        TreeSet<Integer> smalls = new TreeSet<>(comparator);
        TreeSet<Integer> bigs   = new TreeSet<>(comparator);

        double[] result = new double[nums.length - k + 1];

        for (int i = 0; i < nums.length; i++) {
            addNum(i, smalls, bigs);
            if (i + 1 >= k) {
                int start = i - k + 1;
                result[start] = findMedian(smalls, bigs, nums);

                // remove tail index of window, from 1 of the TreeSets
                if (!smalls.remove(start)) {
                    bigs.remove(start);
                }
                // rebalance if necessary
                if (smalls.size() < bigs.size()) {
                    smalls.add(bigs.pollFirst());
                }
            }
        }
        return result;
    }

    private void addNum(int num, TreeSet<Integer> smalls, TreeSet<Integer> bigs) {
        if (smalls.size() == bigs.size()) {
            bigs.add(num);
            smalls.add(bigs.pollFirst());
        } else if (smalls.size() > bigs.size()) {
            smalls.add(num);
            bigs.add(smalls.pollLast());
        } // "smalls" will never be smaller size than "bigs"
    }

    private double findMedian(TreeSet<Integer> smalls, TreeSet<Integer> bigs, int[] nums) {
        if (smalls.isEmpty()) { // ideally should never happen
            return 0;
        } else if (smalls.size() == bigs.size()) {
            return ((double) nums[smalls.last()] + nums[bigs.first()]) / 2;
        } else {
            return nums[smalls.last()];
        }
    }
}
```

### Implementation Details

__Integer Overflow__ - We cast to `double` (when finding median) to avoid integer overflow from addition, which can happen in LeetCode's test cases.

The cast was also necessary to be able to get decimal values when dividing (such as `(3+4)/2 = 3.5`)


### Time/Space Complexity

-  Time Complexity: `O(n log k)`. Add/remove from a TreeSet is O(log k). There are O(n) elements to add/remove.
- Space Complexity: `O(k)` for storage in our TreeSets.
