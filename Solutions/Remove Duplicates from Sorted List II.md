### Notes

This problem is tricky to code correctly. We will use 2 `ListNode` variables to simplify our code:

1. `ListNode dummy` will represent the `ListNode` before the start of the list.
1. `ListNode n` will walk the list and point to 1 `ListNode` before the `ListNode` we're processing. This makes it easier to remove `ListNode`s

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
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode n = dummy;
        while (n.next != null && n.next.next != null) {
            if (n.next.val == n.next.next.val) {
                int duplicate = n.next.val;
                while (n.next != null && n.next.val == duplicate) {
                    n.next = n.next.next;
                }
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
