### Algorithm

1. `k` = # of nodes from beginning of list to beginning of loop
1. `n` = loop size
1. Create a `slow` pointer (moves 1 step at a time) and a `fast` pointer (moves 2 steps at a time) .
1. When `slow` enters loop (after `k` nodes), `fast` is k nodes into the list.
1. That means they will meet in `n - k` steps (Since they get 1 step closer each time).
1. When they meet, `slow` is `n - k` steps into the loop, so `slow` will be at beginning of loop in `k` single steps.
1. Create `slow2` at head of list, and move `slow` and `slow2` 1 step at a time, they will collide in `k` steps, at the head of cycle.

### Provided Code

```java
class ListNode {
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
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) { // they collided
                ListNode slow2 = head;
                while (slow2 != slow) {
                    slow = slow.next;
                    slow2 = slow2.next;
                }
                return slow;
            }
        }
        return null;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n), where n is number of nodes in List.
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/linked-list-cycle-ii/discuss/308124)
- [github.com/RodneyShag](https://github.com/RodneyShag)
