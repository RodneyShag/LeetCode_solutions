### Algorithm

- Let "tail" refer to the first null at the end of the list.
- Create a pointer that iterates through a list.
- When it's at the tail of the list, have it jump to the beginning of the other list.
- Create 2 of these pointers, pointing to 2 different list heads.
- The pointers will collide at the merge point after 1 or 2 passes.
- If they don't collide after 2 passes, then they will both be null, and there is no merge point.

### Provided Code

```java
public class ListNode {
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
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        ListNode a = headA;
        ListNode b = headB;
        while (a != b) {
            a = (a == null) ? headB : a.next;
            b = (b == null) ? headA : b.next;
        }
        return a;
    }
}
```


### Time/Space Complexity

-  Time Complexity: O(m + n)
- Space Complexity: O(1)
