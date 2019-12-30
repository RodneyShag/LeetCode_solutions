### Provided code

```java
class ListNode {
    int val;
    ListNode next;
}
```

### Solution

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode n = head;
        while (n.next != null) {
            if (n.next.val == n.val) {
                n.next = n.next.next; // deletes ListNode
            } else {
                n = n.next;
            }
        }
        return head;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-list/discuss/458403)
- [github.com/RodneyShag](https://github.com/RodneyShag)
