### Notes

- Bottom-up MergeSort
- "stable sort" - the order of equal elements is the same in the input and output
- O(1) space complexity

### Example

If we start off with an input of `4 2 1 3`, we will:
1. Create lists of step size 1, then merge each pair of lists
1. Create lists of step size 2, then merge each pair of lists
1. Create lists of step size 4, then merge each pair of lists

The step size doubles after each merge.


```
[4] [2] [1] [3]   // step size = 1
 [2 4]   [1 3]    // step size = 2
   [1 2 3 4]      // step size = 4
```

### Provided Code

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) {
        val = x;
    }
}
```

### Solution

```java
class MyList {
    ListNode head;
    ListNode tail;
    public MyList(ListNode h, ListNode t) {
        head = h;
        tail = t;
    }
}
```

```java
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        int length = findLength(head);
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        for (int step = 1; step < length; step *= 2) {
            ListNode prev = dummy;
            ListNode curr = dummy.next;
            while (curr != null) {
                ListNode[] lists = getLists(curr, step);
                MyList merged = merge(lists[0], lists[1]);
                prev.next = merged.head;
                prev = merged.tail;
                curr = lists[2];
            }
        }
        return dummy.next;
    }

    private int findLength(ListNode n) {
        int size = 0;
        while (n != null) {
            size++;
            n = n.next;
        }
        return size;
    }

    // returns:
    //    ListNode[0] is list of size: step
    //    ListNode[1] is list of size: step
    //    ListNode[2] is remainder of the list
    private ListNode[] getLists(ListNode curr, int step) {
        if (curr == null || step < 1) { // should never happen
            return null;
        }

        ListNode[] lists = new ListNode[3];

        for (int i = 0; i < 2; i++) {
            if (curr == null) {
                break;
            }
            lists[i] = curr;
            ListNode tail = curr;
            for (int j = 0; j < step; j++) {
                if (curr != null) {
                    tail = curr;
                    curr = curr.next;
                }
            }
            tail.next = null;
        }

        lists[2] = curr;
        return lists;
    }

    private MyList merge(ListNode currA, ListNode currB) {
        if (currA == null || currB == null) {
            return new MyList(currA, currB);
        }

        ListNode dummy = new ListNode(0);
        ListNode n = dummy;
        while (currA != null && currB != null) {
            if (currA.val < currB.val) {
                n.next = currA;
                currA = currA.next;
            } else {
                n.next = currB;
                currB = currB.next;
            }
            n = n.next;
        }

        // attach remaining elements
        n.next = (currA == null) ? currB : currA;

        // find tail of list
        while (n.next != null) {
            n = n.next;
        }

        return new MyList(dummy.next, n);
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n log n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/sort-list/discuss/356829)
- [github.com/RodneyShag](https://github.com/RodneyShag)
