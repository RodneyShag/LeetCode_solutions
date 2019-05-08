### Algorithm

1. Use slow & fast pointers to find middle of list.
1. Reverse the list after the middle point.
1. Merge the 1st half of linked list with the reversed 2nd half we just created.

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
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }

        // find middle of list
        ListNode slow = head;
        ListNode fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        ListNode reversedList = reverseList(slow.next);
        slow.next = null;
        mergeLists(head, reversedList);        
    }

    private ListNode reverseList(ListNode head) {
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

    private ListNode mergeLists(ListNode currA, ListNode currB) {       
        ListNode result = new ListNode(0); // dummy/placeholder ListNode
        ListNode n = result;
        while (currA != null && currB != null) {
            n.next = currA;
            currA = currA.next;
            n = n.next;

            n.next = currB;
            currB = currB.next;
            n = n.next;
        }

        // Attach the remaining element(s)
        if (currA == null) {
            n.next = currB;
        } else {
            n.next = currA;
        }

        return result.next;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)
