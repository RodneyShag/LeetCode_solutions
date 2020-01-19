### Algorithm

- Use a `TreeSet`, as it is kind of like a `Set` and `PriorityQueue` combined
  - the `Set` part will remove duplicates for us
  - the `PriorityQueue` part will keep our elements in sorted order
- If `TreeSet` size grows beyond 3, remove the first (smallest) element in it, so that the 3rd element is always our third maximum number.

### Solution

```java
class Solution {
    public int thirdMax(int[] nums) { // assumes `nums` size is 1 or more
        TreeSet<Integer> ts = new TreeSet();
        for (int n : nums) {
            ts.add(n);
            if (ts.size() > 3) {
                ts.pollFirst();
            }
        }
        return ts.size() < 3 ? ts.last() : ts.first();
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) since `TreeSet` has a fixed size of 3.
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/third-maximum-number/discuss/460676)
- [github.com/RodneyShag](https://github.com/RodneyShag)
