### Algorithm

1. We use 2 Heaps to keep track of median
    - maxHeap contains all SMALL elements
    - minHeap contains all LARGE elements
1. We make sure that 1 of the following conditions is always true:
    - maxHeap.size() == minHeap.size()
    - maxHeap.size() - 1 = minHeap.size()

### Solution

```java
class MedianFinder {
    private Queue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    private Queue<Integer> minHeap = new PriorityQueue();

    public void addNum(int num) {
        if (maxHeap.size() == minHeap.size()) {
            minHeap.add(num);
            maxHeap.add(minHeap.remove());
        } else if (maxHeap.size() > minHeap.size()) {
            maxHeap.add(num);
            minHeap.add(maxHeap.remove());
        } // maxHeap will never be smaller size than minHeap
    }

    public double findMedian() {
        if (maxHeap.isEmpty()) {
            return 0;
        } else if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        } else {
            return maxHeap.peek();
        }
    }
}
```

### Time Complexity

O(log n) for addNum(). O(1) for findMedian()

### Space Complexity

- O(1) for storage of each number
- O(1) for addNum()
- O(1) for findMedian()

### Alternate Solution

Instead of 2 heaps, you can use a self-balancing Binary Search Tree (like an AVL Tree). See [LeetCode Solution - Approach 4: Multiset and Two Pointers](https://leetcode.com/problems/find-median-from-data-stream/solution/) for an excellent explanation. Unfortunately it does not seem that Java has a `Multiset` for us to use.

### Followup #1 - If all integer numbers from the stream are between 0 and 100, how would you optimize it

1. Create 101 buckets using an array of size 101.
1. Store the numbers into these buckets.
1. Find median by looping through this array.


- Time Complexity
  - addNum() is O(1)
  - findMedian() is O(1) since array has fixed size.
- Space Complexity: O(1) since array has fixed size.
- Sample problem: https://leetcode.com/problems/statistics-from-a-large-sample/description/

### Followup #2 - If 99% of all integer numbers from the stream are between 0 and 100, how would you optimize it?

1. Divide problem into 3 subproblems. Here are the groupings:
    1. __Numbers < 0__: You have 2 options:
		    1. Use 2-heap solution (that we coded in original solution), or
	    	1. Use 1 array, which represents 1 bucket
    1. __0 <= Numbers <= 100__: Use 100 buckets using an array of size 100
    1. __100 < Numbers__: You have 2 options:
	    	1. Use 2-heap solution (that we coded in original solution), or
		    1. Use 1 array, which represents 1 bucket
1. For each number we get in the stream, insert it into 1 of the 3 groupings, keeping track of the count of numbers in each of these 3 groupings
1. To find the median, see which grouping the median must fall into and find it there.

For __Numbers < 0__ and __100 < Numbers__, using 2 arrays/buckets is the more practical solution since it is very unlikely the median will fall into either bucket/array. This makes findMedian() O(1) in average case. In the worst case, all numbers fall in 1 array, and we would either have to use Quickselect (O(n) average case, O(n<sup>2</sup>) worst case), or sorting (O(n log n)) to find the median.

If you use 2 heaps instead, you will get findMedian() of O(1) average case, O(log n) worst case.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/find-median-from-data-stream/discuss/343662)
- [github.com/RodneyShag](https://github.com/RodneyShag)
