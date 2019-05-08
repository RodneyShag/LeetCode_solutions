### Algorithm

1. Create a pointer that moves 1 step  at a time: `slow`
1. Create a pointer that moves 2 steps at a time: `fast`
1. If the Linked List has a cycle, `slow` and `fast` will collide.

### Provided code

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) {
        val = x;
        next = null;
    }
}
```

### Solution

```java
class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) {
            return false;
        }

        ListNode slow = head; // moves 1 ListNode  at a time
        ListNode fast = head; // moves 2 ListNodes at a time

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true; // "slow" and "fast" collided, so we must have a cycle.
            }
        }
        return false;
    }
}
```
### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)
