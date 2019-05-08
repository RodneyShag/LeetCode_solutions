### Provided code

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}
```

### Solution

```java
class Solution {
    public ListNode mergeTwoLists(ListNode currA, ListNode currB) {
        if (currA == null) {
            return currB;
        } else if (currB == null) {
            return currA;
        }

        ListNode result = new ListNode(0); // dummy/placeholder ListNode
        ListNode n = result;
        while (currA != null && currB != null) {
            if (currA.val < currB.val) {
                n.next = currA;
                currA = currA.next;
            } else {
                n.next = currB;
                currB = currB.next;
            }
            n = n.next;
        }

        // Attach the remaining elements
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

- Time Complexity: O(n + m)
- Space Complexity: O(1)
