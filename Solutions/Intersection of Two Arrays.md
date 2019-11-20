### Algorithm

1. Make a `Set` with numbers from `nums1`
1. Make a `Set` with numbers from `nums2`
1. The "set union" of these 2 sets is our solution. In Java we use the `retainAll()` for set union.
1. Since our return value must be an array, convert our solution set into an array.

### Solution

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set1 = new HashSet();
        for (Integer n : nums1) {
            set1.add(n);
        }
        Set<Integer> set2 = new HashSet();
        for (Integer n : nums2) {
            set2.add(n);
        }

        set1.retainAll(set2); // set1 becomes union of set1 and set2

        int[] output = new int[set1.size()];
        int i = 0;
        for (int num : set1) {
            output[i++] = num;
        }
        return output;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n + m)
- Space Complexity: O(n + m)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/intersection-of-two-arrays/discuss/432767)
- [github.com/RodneyShag](https://github.com/RodneyShag)
