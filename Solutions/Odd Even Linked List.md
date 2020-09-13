### Algorithm

- Create 2 `ListNode` pointers that will walk the original list
  -  `odd` will build the  odd list
  - `even` will build the even list
- We also need to keep track of both list heads
  - `head` will keep track of the odd list head
  - `ListNode evenHead` (which we will create) will keep track of the even list head
- After we build both lists, connect the even list to the end of the odd list

### Example

- Let `o` represent the  `odd` pointer.
- Let `e` represent the `even` pointer.
- This is how we intend `o` and `e` to traverse the list:

```
1 -> 2 -> 3 -> 4 -> 5 -> null
o    e

1 -> 2 -> 3 -> 4 -> 5 -> null
          o    e

1 -> 2 -> 3 -> 4 -> 5 -> null
                    o    e
```

except that we will be building an odd list and even list while traversing

### Provided code

```java
class ListNode {
    ListNode next;
}
```

### Solution

```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null) {
            return head;
        }
        ListNode odd = head;
        ListNode even = head.next;
        ListNode evenHead = even;
        while (even != null && even.next != null) {
            odd.next = even.next;
            odd = odd.next;
            even.next = odd.next;
            even = even.next;
        }
        odd.next = evenHead;
        return head;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
