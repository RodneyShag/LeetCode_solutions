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
        if (m == null) {
            return m;
        } else if (n == null) {
            return n;
        }

        Stack<Integer> stack1 = new Stack<>();
        Stack<Integer> stack2 = new Stack<>();

        while (m != null) {
            stack1.push(m.val);
            m = m.next;
        }
        while (n != null) {
            stack2.push(n.val);
            n = n.next;
        }

        int carry = 0;
        ListNode dummy = new ListNode(0); // 1 Node before the actual head of list
        while (!stack1.isEmpty() || !stack2.isEmpty() || carry != 0) {
            int value = carry;
            if (!stack1.isEmpty()) {
                value += stack1.pop();
            }
            if (!stack2.isEmpty()) {
                value += stack2.pop();
            }
            int digit = value % 10;
            carry = value / 10;
            ListNode head = new ListNode(digit);
            head.next = dummy.next;
            dummy.next = head;
        }
        return dummy.next;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(m + n)
- Space Complexity: O(m + n)
