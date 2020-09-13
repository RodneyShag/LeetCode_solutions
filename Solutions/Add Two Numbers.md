### Provided Code

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
    public ListNode addTwoNumbers(ListNode m, ListNode n) {
        int carry = 0;
        ListNode dummy = new ListNode(0); // 1 Node before the actual head of list
        ListNode tail = dummy;
        while (m != null || n!= null || carry != 0) {
            int value = carry;
            if (m != null) {
                value += m.val;
                m = m.next;
            }
            if (n != null) {
                value += n.val;
                n = n.next;
            }
            int digit = value % 10;
            carry = value / 10;
            tail.next = new ListNode(digit);
            tail = tail.next;
        }
        return dummy.next;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(m + n)
- Space Complexity: O(m + n)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
