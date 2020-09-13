### Hint

Create a `ListNode dummy`, where `dummy.next = head`. This will make it easier to remove elements at the head of the list, if necessary.

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
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode n = dummy;
        while (n.next != null) {
            if (n.next.val == val) {
                n.next = n.next.next;
            } else {
                n = n.next;
            }
        }        
        return dummy.next;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
