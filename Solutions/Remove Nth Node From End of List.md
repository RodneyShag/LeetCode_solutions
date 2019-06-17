### Algorithm

1. Find the size of the list by walking through entire list.
1. Do `size - n - 1` to see how many steps you should take before removing the next node.
1. Walk that many steps and remove the node.
1. Return the head of the list.

### Solution

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        int size = findSize(head);
        if (n == size) {
            return head.next;
        } else {
            int steps = size - n - 1;
            ListNode node = head;
            while (steps-- > 0) {
                node = node.next;
            }
            node.next = node.next.next; // remove node
            return head;
        }
    }

    private int findSize(ListNode head) {
        ListNode n = head;
        int size = 0;
        while (n != null) {
            size++;
            n = n.next;
        }
        return size;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Follow-up Solution

There is no benefit in solving this problem in 1 pass instead of 2 passes, as the time and space complexity remain the same. In both solutions, you would still have to traverse every element in the list.
