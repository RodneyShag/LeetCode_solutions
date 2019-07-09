### Algorithm

Suppose we are given list [1,2,3,4,5], m=2, n=4 (where m, n are 1-indexed instead of 0-indexed).

```
   |-------|
1->|2->3->4|->5
   |-------|

```
We want to reverse 2->3->4 to get

```
   |-------|
1->|4->3->2|->5
   |-------|
```
1. For the boxed part above, we will use a standard [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) algorithm.
1. To be able to connect the reversed box to the `1->` and the `->5`, we will keep 2 additional variables: `left` and `right`.
    - `left` will point to `1` (For 1st picture above, the 1st element before the box)
    - `right` will point to `2` (For 1st picture above, the 1st element in the box)

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

Problem statement guarantees valid input of `1 <= m <= n <= length of list`, so we will skip error checking on input.

```java
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (m == n) {
            return head;
        }

        // Find beginning part of the list we want to reverse
        ListNode prev = head;
        ListNode left = null;
        for (int i = 1; i < m; i++) {
            left = prev;
            prev = prev.next;
        }
        ListNode right = prev;

        // Reverse indices [m,n] of list iteratively
        ListNode curr = prev.next;
        ListNode next = null;
        int numReverses = n - m;
        while (curr != null && numReverses-- > 0) {
            next = curr.next;
            curr.next = prev; // changes arrow direction
            prev = curr;
            curr = next;
        }

        // Fix connections and return head of list
        right.next = next;
        if (left == null) {
            return prev;
        } else {
            left.next = prev;            
            return head;
        }
    }
}
```

### Implementation Details

For `while (curr != null && numReverses-- > 0)` above, `curr` will never be null since problem guarantees `1 <= m <= n <= length of list`

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)
