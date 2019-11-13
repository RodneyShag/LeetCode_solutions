### Algorithm

1. Create a Set of elements with values 1 to n (inclusive)
1. Loop through input array to remove corresponding elements from our Set.

### Solution

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        Set<Integer> set = new HashSet();
        for (int i = 1; i <= nums.length; i++) {
            set.add(i);
        }
        for (int num : nums) {
            set.remove(num);
        }
        return new ArrayList(set);
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

### Follow-up Question

The follow-up question asks to "do it without extra space and O(n) runtime", but since we still need O(n) space for the returned list, I don't see a practical reason to solve this problem with the follow-up added restriction.
