### Algorithm

1. Make a `Map` with numbers from `nums1`
    - "key" is number
    - "value" is how many times it appears in `nums1`
1. Loop through `nums2` to see which numbers match with `Map` representing `nums1`
1. Since our return value must be an array, convert our solution set into an array.

### Solution

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null) {
            return new int[0];
        }
        Map<Integer, Integer> map = new HashMap();
        for (Integer n : nums1) {
            map.merge(n, 1, Integer::sum);
        }

        List<Integer> intersection = new ArrayList();
        for (int n : nums2) {
            if (map.containsKey(n) && map.get(n) > 0) {
                intersection.add(n);
                map.merge(n, -1, Integer::sum);
            }
        }

        int[] result = new int[intersection.size()];
        for (int i = 0; i < result.length; i++) {
            result[i] = intersection.get(i);
        }
        return result;
    }
}
```

### Time/Space Complexity

-  Time Complexity: `O(m + n)`
- Space Complexity: `O(m + n)`

### Follow-up 1

__What if the given array is already sorted? How would you optimize your algorithm?__

If the arrays are already sorted, we can use 2 pointers to traverse

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null) {
            return new int[0];
        }
        Arrays.sort(nums1);
        Arrays.sort(nums2);

        List<Integer> intersection = new ArrayList();

        for (int i = 0, j = 0; i < nums1.length && j < nums2.length;  ) {
            if (nums1[i] == nums2[j]) {
                intersection.add(nums1[i]);
                i++;
                j++;
            } else if (nums1[i] < nums2[j]) {
                i++;
            } else {
                j++;
            }
        }

        int[] result = new int[intersection.size()];
        for (int i = 0; i < result.length; i++) {
            result[i] = intersection.get(i);
        }
        return result;
    }
}
```

-  Time Complexity: `O(m + n)` if arrays are already sorted for us.
- Space Complexity: `O(m + n)`

### Follow-up 2

__What if nums1's size is small compared to nums2's size? Which algorithm is better?__

If the arrays are not sorted, then the `HashMap` solution is faster.

If the arrays are sorted, then we can loop through `nums1` (the smaller array), and for each value, binary search it in `nums2` (the larger array). Implementation becomes tricky if duplicate values are allowed. To deal with duplicates, we alter binary search so that if duplicates exist, we return the index for the match furthest left.

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null) {
            return new int[0];
        } else if (nums1.length > nums2.length) {
            return intersect(nums2, nums1); // ensures 1st array is shorter than 2nd.
        }
        Arrays.sort(nums1);
        Arrays.sort(nums2);

        List<Integer> intersection = new ArrayList();
        int leftIndex = 0;
        for (int i = 0; i < nums1.length; i++) {
            Integer index = binarySearch(nums2, nums1[i], leftIndex);
            if (index != null) {
                intersection.add(nums1[i]);
                leftIndex = index + 1;
            }
        }

        int[] result = new int[intersection.size()];
        for (int i = 0; i < result.length; i++) {
            result[i] = intersection.get(i);
        }
        return result;
    }

    // binary search from 'lo' to end of array
    private Integer binarySearch(int[] sortedArray, int value, int lo) {
        int hi = sortedArray.length - 1;
        while (lo <= hi) {
            int mid = (lo + hi) / 2;
            if (sortedArray[mid] > value) {
                hi = mid - 1;
            } else if (sortedArray[mid] < value) {
                lo = mid + 1;
            } else {
                // if duplicates exist, return the index for the match furthest left.
                while (mid > lo && sortedArray[mid - 1] == value) {
                    mid--;
                }
                return mid;
            }
        }
        return null;
    }
}
```

-  Time Complexity: `O(m log n)` if arrays are already sorted for us, where `m` is size of smaller array and `n` is size of larger array
- Space Complexity: `O(m)` to generate the intersection

### Follow-up 3

__What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?__

1. Use a `Map` to store `nums1`.
1. Divide `nums2` into `n` chunks of `1/n` size.
1. Bring 1 chunk at a time of `nums2` into memory and see if it intersects with our `Map`. If the intersection we're generating gets too big to fit in memory, we can save our partial solution to disk and continue with our algorithm.

### Follow-up 4 (Custom)

__What if neither nums1 or nums2 can fully fit in memory?__

1. Use [external sort](https://en.wikipedia.org/wiki/External_sorting) to sort `nums1`
1. Use [external sort](https://en.wikipedia.org/wiki/External_sorting) to sort `nums2` (this step can theoretically be done in parallel to the above step)
1. Use the 2-pointer solution above to create our solution
    - Divide `nums1` into chunks that can fit in memory without consuming over ~10% of it
    - Divide `nums2` into chunks that can fit in memory without consuming over ~10% of it
    - The resulting ~80% can be used for our generated intersection
    - Bring in 1 chunk of `nums1` and 1 chunk of `nums2` into memory together
    - If the intersection we're generating gets too big to fit in memory, we can save our partial solution to disk and continue with our algorithm


### Links

- [Discuss on LeetCode](https://leetcode.com/problems/intersection-of-two-arrays-ii/discuss/439955)
- [github.com/RodneyShag](https://github.com/RodneyShag)
