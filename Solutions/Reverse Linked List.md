### Notes

Iterative solution using 3 pointers.

### Provided code

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
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode prev = null;
        ListNode curr = head;
        ListNode next = null;
        while (curr != null) {
            next = curr.next;
            curr.next = prev; // changes arrow direction
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)
