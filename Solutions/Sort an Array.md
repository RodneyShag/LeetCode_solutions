### Algorithm

Use [HeapSort](https://en.wikipedia.org/wiki/Heapsort#Algorithm)

A heap is represented as a tree. We can also store it as a 1-dimensional array:

```
       2
    /     \
   3       6      becomes array: [2 3 6 8 4 9 7]
  / \     / \
 8   4   9   7  
```

In the 1-dimensional array, these formulas let us find leftChild, rightChild, and parent:

```
iLeftChild(i)  = 2*i + 1
iRightChild(i) = 2*i + 2
iParent(i)     = floor((i-1) / 2)
```

1. [Build a max heap](https://en.wikipedia.org/wiki/Binary_heap#Building_a_heap)
1. Convert heap to sorted list. Do this by repeating these steps for all elements:
    1. Swap the maximum (0th) element in our heap with element at end of array.
    1. Decrease array size by 1. All elements from 0 to this new `end` represent our new heap.
    1. Restore our heap structure by "bubbling down" the newly misplaced 0th element into its correct position

### Code

Code is adapted from [Wikipedia - Heapsort](https://en.wikipedia.org/wiki/Heapsort#Pseudocode)

```java
class Solution {
    public int[] sortArray(int[] A) {
        if (A == null || A.length <= 1) {
            return A;
        }
        buildMaxHeap(A);
        convertHeapToSortedList(A);
        return A;
    }

    private void buildMaxHeap(int[] A) {
        int start = iParent(A.length - 1);
        while (start >= 0) {
            bubbleDown(A, start, A.length - 1);
            start--;
        }
    }

    private void convertHeapToSortedList(int[] A) { // assumes input is a valid heap
        int end = A.length - 1;
        while (end > 0) {
            swap(A, 0, end);
            end--;
            bubbleDown(A, 0, end);
        }
    }

    private void bubbleDown(int[] A, int start, int end) {
        int curr = start;
        while (hasChild(curr, end)) {
            int maxChildIndex = maxChild(A, curr, end);
            if (A[maxChildIndex] > A[curr]) {
                swap(A, curr, maxChildIndex);
                curr = maxChildIndex;
            } else {
                return;
            }
        }
    }

    private int iLeftChild(int i) {
        return 2*i + 1;
    }

    private int iRightChild(int i) {
        return 2*i + 2;
    }

    private int iParent(int i) {
        return (i - 1) / 2;
    }

    private boolean hasChild(int curr, int end) {
        return iLeftChild(curr) <= end;
    }

    private int maxChild(int[] A, int i, int end) { // assumes left child exists
        if (iRightChild(i) > end) {
            return iLeftChild(i);
        } else if (A[iLeftChild(i)] > A[iRightChild(i)]) {
            return iLeftChild(i);
        } else {
            return iRightChild(i);
        }
    }

    private void swap(int[] A, int x, int y) {
        int temp = A[x];
        A[x] = A[y];
        A[y] = temp;
    }
}
```

### Time/Space Complexity

- Time Complexity: `O(n log n)`
    - building a heap is `O(n)` [according to this mathematical proof](https://en.wikipedia.org/wiki/Binary_heap#Building_a_heap).
    - converting the heap to a sorted list is `O(n log n)` since we remove the minimum in `O(1)`, and restore the heap in `O(log n)`. We do this `n` times.
- Space Complexity: `O(1)`

### [Comparison with other sorts](https://en.wikipedia.org/wiki/Heapsort#Comparison_with_other_sorts)

The linux Kernel uses Heapsort.

- Merge sort on arrays has considerably better data cache performance, often outperforming heapsort on modern desktop computers because merge sort frequently accesses contiguous memory locations (good [locality of reference](https://en.wikipedia.org/wiki/Locality_of_reference)); heapsort references are spread throughout the heap.
- Heapsort is not a [stable sort](https://en.wikipedia.org/wiki/Sorting_algorithm#Stability); merge sort is stable.
- Merge sort parallelizes well and can achieve close to linear speedup with a trivial implementation; heapsort is not an obvious candidate for a parallel algorithm.
- Merge sort [parallelizes](https://en.wikipedia.org/wiki/Parallel_algorithm) well and can achieve close to [linear speedup](https://en.wikipedia.org/wiki/Speedup) with a trivial implementation; heapsort is not an obvious candidate for a parallel algorithm.
- Merge sort is used in [external sorting](https://en.wikipedia.org/wiki/External_sorting); heapsort is not. Locality of reference is the issue.
