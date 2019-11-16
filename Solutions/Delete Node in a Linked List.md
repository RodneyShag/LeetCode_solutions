### Assumptions from Problem Description

1. "The given node will not be the tail and it will always be a valid node of the linked list" - Our trick below only works if the input node is not the tail of the list
1. "The linked list will have at least two elements" -  However, we still check for 2+ element lists in the code

### Provided Code

```java
public class ListNode {
    int val;
    ListNode next;
}
```

### Solution

```java
class Solution {
   public void deleteNode(ListNode n) {
       if (n == null || n.next == null) {
           return;
       }
       n.val = n.next.val;
       n.next = n.next.next;
   }
}
```

### Time/Space Complexity

- Time Complexity: O(1)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/delete-node-in-a-linked-list/discuss/312458)
- [github.com/RodneyShag](https://github.com/RodneyShag)
