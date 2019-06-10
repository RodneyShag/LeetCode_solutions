### Algorithm

1. Reverse 2nd half of list
1. Compare 1st half of list to 2nd half

### Provided code

```java
public class ListNode {
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
    public boolean isPalindrome(ListNode head) {
        if (head == null) {
            return true; // LeetCode expects 'true' here
        }

        // Reverse 2nd half of list
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        if (fast != null) { // for lists with odd # of Nodes
            slow = slow.next;
        }
        ListNode slowCenter = reverseList(slow);

        // compare 1st half of list to 2nd half
        ListNode slowFront = head;
        while (slowCenter != null) {
            if (slowCenter.val != slowFront.val) {
                return false;
            }
            slowFront = slowFront.next;
            slowCenter = slowCenter.next;
        }
        return true;
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
}
```

### Preserving Input List Order

Our code destroyed the ordering of the original list. If we wanted to preserve the ordering, we would simply re-reverse the 2nd half of the list to return the input to its original state.

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Alternative Solution 1 - O(n) time, O(n) space

1. Save 1st half of list in stack
1. Compare 2nd half of list to 1st half of list

### Alternative Solution 2 - O(n) time, O(n) space

1. Deep copy list.
1. Reverse it.
1. Compare it to original.
