### Notes

- Use 1 stack for each Linked List to reverse each Linked List. It will now be easier to add numbers in the lists.
- I use an `ArrayDeque` as a `Stack` since it's faster.

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
            return n;
        } else if (n == null) {
            return m;
        }

        Deque<Integer> deque1 = new ArrayDeque(); // use as a stack
        Deque<Integer> deque2 = new ArrayDeque(); // use as a stack

        while (m != null) {
            deque1.push(m.val);
            m = m.next;
        }
        while (n != null) {
            deque2.push(n.val);
            n = n.next;
        }

        int carry = 0;
        ListNode dummy = new ListNode(0); // 1 Node before the actual head of list
        while (!deque1.isEmpty() || !deque2.isEmpty() || carry != 0) {
            int value = carry;
            if (!deque1.isEmpty()) {
                value += deque1.pop();
            }
            if (!deque2.isEmpty()) {
                value += deque2.pop();
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

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/add-two-numbers-ii/discuss/307030)
- [github.com/RodneyShag](https://github.com/RodneyShag)
