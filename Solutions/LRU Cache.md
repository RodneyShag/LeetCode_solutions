### Algorithm

- Create a `Node` class.
  - We will store both a 'key' and a 'value' in this Node (I will provide the reasoning behind this later below)
- Create a `DoublyLinkedList` class
  - We will use "dummy" nodes for the "head" and "tail". This will let us omit `head == null` checks for adding to the list, which also improves performance on the common operation of inserting into our list.
  - This class will be used to maintain ordering. The 1st element in the list represents the most "recently used" Node.
  - We create a Doubly-Linked instead of Singly-Linked list so that, given access to a Node in the list, we can remove it.
- Create a `Map<Integer, Node>`
  - Since we don't have O(1) access to elements in our `DoublyLinkedList`, our `HashMap` will provide us with this O(1) access using a 'key' for each `Node`.


__A Node needs a 'value', but why store a 'key' there as well?__ Because when we remove from end of Linked List, the Node's key is used to find the Node in the HashMap (to remove the node there as well).

There is also an excellent explanation in "Cracking the Coding Interview", 6th Edition solutions.

### Solution

```java
class Node { // public variables for simplicity
    int key;
    int value;
    Node next;
    Node prev;

    public Node(int k, int v) {
        key = k;
        value = v;
        next = null;
        prev = null;
    }
}
```

```java
class DoublyLinkedList {
    private Node head = new Node(0, 0); // dummy node
    private Node tail = new Node(0, 0); // dummy node

    public DoublyLinkedList() {
        head.next = tail;
        tail.prev = head;
    }

    public void addFirst(Node n) {
        if (n == null) {
            return;
        }
        n.prev = head;
        n.next = head.next;
        head.next.prev = n;
        head.next = n;
    }

    public void remove(Node n) { // Assumes 'n' is in this list
        if (n == null || n.prev == null || n.next == null) {
            return;
        }
        n.prev.next = n.next;
        n.next.prev = n.prev;
    }

    public Node getFirst() {
        if (head.next == tail) {
            return null; // list has 0 Nodes
        }
        return head.next;
    }

    public Node getLast() {
        if (head.next == tail) {
            return null; // list has 0 Nodes
        }
        return tail.prev;
    }
}
```

```java
class LRUCache {
    private int capacity;
    private Map<Integer, Node> map; // gives us O(1)-time access to Nodes
    private DoublyLinkedList dll;   // used to keep track of "freshness" of Nodes

    public LRUCache(int capacity) {
        this.capacity = (capacity < 1) ? 1 : capacity;
        map = new HashMap<>();
        dll = new DoublyLinkedList();
    }

    public void put(int key, int value) {
        remove(key); // If key already exists, we will overwrite it.
        if (map.size() >= capacity) {
          remove(dll.getLast().key);
        }
        Node n = new Node(key, value);
        dll.addFirst(n);
        map.put(key, n);
    }

    public int get(int key) {
        Node n = map.get(key);
        if (n == null) {
            return -1; // Problem wants -1 returned. It's better to throw Exception instead.
        }
        if (n != dll.getFirst()) {
            updateFreshness(n);
        }
        return n.value;
    }

    public void remove(int key) {
        Node n = map.get(key);
        dll.remove(n);
        map.remove(key);
    }

    private void updateFreshness(Node n) { // Assumes 'n' is in this list
        dll.remove(n);
        dll.addFirst(n);
    }
}
```

### Time/Space Complexity
-  Time Complexity: `put()`, `get()`, `remove()` are O(1) time
- Space Complexity: Depends on cache size. Can make it as big as we want.

### Alternative Solution

Java has an LRU cache available - it is just a [LinkedHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html) with an "accessOrder" flag set to "true". This will create an LRU cache for you. The [Android source code](https://android.googlesource.com/platform/frameworks/support.git/+/795b97d901e1793dac5c3e67d43c96a758fec388/v4/java/android/support/v4/util/LruCache.java) uses a `LinkedHashMap` to create an LRU cache as well.

A concise `LinkedHashMap` solution is found [here](https://leetcode.com/problems/lru-cache/discuss/45939/Laziest-implementation%3A-Java's-LinkedHashMap-takes-care-of-everything), but this solution is likely not what the interviewer is looking for.
