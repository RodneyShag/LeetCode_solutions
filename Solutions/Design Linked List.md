### Notes

We will use 2 pointers, `head` and `tail`, so that inserting at the end of a list (which is a common operation) can be done in O(1) time.

### Solution

```java
class Node { // public variables used for simplicity
    Node next = null;
    int val = 0;

    public Node(int v) {
        val = v;
    }
}

class MyLinkedList { // Singly-Linked List
    private Node head = null;
    private Node tail = null;
    private int size = 0;

    public int get(int index) {
        if (index < 0 || index >= size) {
            return -1;
        }
        Node curr = head;
        for (int i = 0; i < index; i++) {
            curr = curr.next;
        }
        return curr.val;
    }

    public void addAtHead(int val) {
        Node n = new Node(val);
        if (size == 0) {
            head = n;
            tail = n;
        } else {
            n.next = head;
            head = n;
        }
        size++;
    }

    public void addAtTail(int val) {
        Node n = new Node(val);
        if (size == 0) {
            head = n;
            tail = n;
        } else {
            tail.next = n;
            tail = n;
        }
        size++;
    }

    public void addAtIndex(int index, int val) {
        if (index > size) {
            return;
        }

        if (index <= 0) {   // "If index is negative,
            addAtHead(val); // the node will be inserted at the head of the list."
        } else if (index == size) {
            addAtTail(val);
        } else {
            Node n = new Node(val);
            Node curr = head;
            for (int i = 0; i < index - 1; i++) {
                curr = curr.next;
            }
            n.next = curr.next;
            curr.next = n;
            size++;
        }
    }

    public void deleteHead() {
        if (size > 0) {
            head = head.next;
            size--;
            if (size == 0) {
                tail = null;
            }
        }
    }

    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }

        if (index == 0) {
            deleteHead();
        } else {
            Node curr = head;
            for (int i = 0; i < index - 1; i++) {
                curr = curr.next;
            }
            if (curr.next == tail) {
                tail = curr;
            }
            curr.next = curr.next.next;
            size--;
        }
    }
}
```

### Time Complexity

- get(): O(n)
- addAtHead(): O(1)
- addAtTail(): O(1)
- addAtIndex(): O(n)
- deleteHead(): O(1)
- deleteAtIndex(): O(n)

### Space Complexity

- Each node uses O(1) storage.
- Calls to each function above takes O(1) space

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/design-linked-list/discuss/343580)
- [github.com/RodneyShag](https://github.com/RodneyShag)
