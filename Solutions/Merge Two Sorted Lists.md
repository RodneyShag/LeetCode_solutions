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
    public ListNode mergeTwoLists(ListNode currA, ListNode currB) {
        if (currA == null) {
            return currB;
        } else if (currB == null) {
            return currA;
        }

        ListNode dummy = new ListNode(0);
        ListNode n = dummy;
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

        // attach remaining elements
        n.next = (currA == null) ? currB : currA;

        return dummy.next;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n + m)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/merge-two-sorted-lists/discuss/304545)
- [github.com/RodneyShag](https://github.com/RodneyShag)
