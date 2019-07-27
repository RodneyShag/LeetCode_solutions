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
    private PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    private PriorityQueue<Integer> minHeap = new PriorityQueue<>();

    public void addNum(int num) {
        if (maxHeap.isEmpty()) {
            maxHeap.add(num);
        } else if (maxHeap.size() == minHeap.size()) {
            minHeap.add(num);
            maxHeap.add(minHeap.remove());
        } else if (maxHeap.size() > minHeap.size()) {
            maxHeap.add(num);
            minHeap.add(maxHeap.remove());
        }
        // maxHeap will never be smaller size than minHeap
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

We will combine the above 2 solutions to create this solution

1. Divide problem into 3 subproblems. Here are the groupings:
    1. __Numbers < 0__: Use 2-heap solution (that we coded in original solution)
    1. __0 <= Numbers <= 100__: Use 101 buckets using an array of size 101
    1. __100 < Numbers__: Use 2-heap solution (that we coded in original solution)
1. For each number we get in the stream, insert it into 1 of the 3 groupings, keeping track of the count of numbers in each of these 3 groupings
1. To find the median, see which grouping the median must fall into and find it there.

Since this solution is a combination of our original coded solution, and Followup #1, the time/space complexity analysis is the same as for those solutions
