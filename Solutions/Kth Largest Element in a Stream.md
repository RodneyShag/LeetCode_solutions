### Algorithm

Use a min heap (which in Java is a `PriorityQueue`) to keep track of the `k` largest numbers, where the minimum of the min heap will represent the `k-th` largest number

### Example

Here is the sample input from the problem:
```
int k = 3;
int[] arr = [4,5,8,2];
KthLargest kthLargest = new KthLargest(3, arr);
kthLargest.add(3);   // returns 4
kthLargest.add(5);   // returns 5
kthLargest.add(10);  // returns 5
kthLargest.add(9);   // returns 8
kthLargest.add(4);   // returns 8
```

Each line below corresponds to reading in 1 input from the stream. The brackets [] are used to show the values in the min heap:
```
[4]
[4 5]
[4 5 8]
2 [4 5 8]            // at this step, constructor has finished executing
2 3 [4 5 8]          // returns 4
2 3 4 [5 5 8]        // returns 5
2 3 4 5 [5 8 10]     // returns 5
2 3 4 5 5 [8 9 10]   // returns 8
2 3 4 4 5 5 [8 9 10] // returns 8
```

### Solution

```java
class KthLargest {
    private Queue<Integer> pq;
    private int k;

    public KthLargest(int k, int[] nums) {
        pq = new PriorityQueue<>(k);
        this.k = k;
        for (int num : nums) {
            add(num);
        }
    }

    public int add(int val) {
        pq.add(val);
        if (pq.size() == k + 1) {
            pq.remove();
        }
        return pq.peek();
    }
}
```

### Time Complexity

- add() is O(log k)
- the constructor KthLargest() is O(n log k)

### Space Complexity

O(k) due to the size of the heap.
