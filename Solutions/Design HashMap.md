# Solution 1 - HashMap with rehash

### Hints

1. Create a `Cell` class
1. Represent `MyHashMap` as an ArrayList of LinkedLists of Cells

### Code

```java
class Cell { // public variables for simplicity.
    int key;
    int value;

    public Cell(int k, int v) {
        key = k;
        value = v;
    }
}
```

```java
class MyHashMap {
    private int numBuckets = 100;
    private ArrayList<LinkedList<Cell>> lists = new ArrayList<>(numBuckets);
    private final double LOAD_FACTOR = 0.7;
    private int numItems = 0;

    public MyHashMap() {
        initializeLists(lists);
    }

    private void initializeLists(ArrayList<LinkedList<Cell>> lists) {
        for (int i = 0; i < numBuckets; i++) {
            lists.add(new LinkedList());
        }
    }

    private int createHashCode(int key) {
        return key % numBuckets;
    }

    public void put(int key, int value) {
        // Find the LinkedList that we should put the Cell into.
        int hashCode = createHashCode(key);
        LinkedList<Cell> list = lists.get(hashCode);

        // See if we should overwrite an old Cell.
        for (Cell cell : list) {
            if (cell.key == key) {
                cell.value = value; // overwrites the old value.
                return;
            }
        }

        // Create new Cell and add it to our LinkedList.
        list.add(new Cell(key, value));
        numItems++;

        // Rehash if our load factor is too high.
        double loadFactor = (double) numItems / numBuckets;
        if (loadFactor > LOAD_FACTOR) {
            rehash();
        }
    }

    public int get(int key) {
        // Find the LinkedList that may contain the value.
        int hashCode = createHashCode(key);
        LinkedList<Cell> list = lists.get(hashCode);

        for (Cell cell : list) {
            if (cell.key == key) {
                return cell.value;
            }
        }
        // key doesn't exist.
        return -1; // Fine since "keys/values are in range of [0, 1000000]"
    }

    public void remove(int key) {
        // Find the LinkedList that may contain the value.
        int hashCode = createHashCode(key);
        LinkedList<Cell> list = lists.get(hashCode);

        for (int i = 0; i < list.size(); i++) {
            if (list.get(i).key == key) {
                list.remove(i);
                numItems--;
                return;
            }
        }
    }

    private void rehash() {
        ArrayList<LinkedList<Cell>> temp = lists;
        numBuckets *= 2;
        lists = new ArrayList<>(numBuckets);
        initializeLists(lists);
        numItems = 0;
        for (LinkedList<Cell> list : temp) {
            for (Cell cell : list) {
                put(cell.key, cell.value);
            }
        }
    }
}
```
### Additional Notes

If the key/value pairs weren't integers, we could create a parameterized `Cell<K, V>` class instead of the simpler `Cell` class.

### Time/Space Complexity

-  Time complexity: O(1) average and O(n) worst case for get(), put() and remove().
- Space complexity: O(n), where n is number of entries in `MyHashMap`.


# Solution 2 - Using Giant Array

This problem is unique in that the keys are in the range [0, 1000000]. We can exploit this fact and just use a giant array to represent our HashMap, like in [Solution 2 here](https://leetcode.com/problems/design-hashmap/discuss/227081/Java-Solutions)

### Code

```java
class MyHashMap {
    int[] map;

    public MyHashMap() {
        map = new int[1000001];
        Arrays.fill(map,-1);
    }

    public int get(int key) {
        return map[key];
    }

    public void put(int key, int value) {
        map[key] = value;
    }

    public void remove(int key) {
        map[key] = -1;
    }
}
```

### Time/Space Complexity

-  Time complexity: O(1) average and O(n) worst case for get(), put() and remove().
- Space complexity: O(n).

# Links

- [Discuss on LeetCode](https://leetcode.com/problems/design-hashmap/discuss/346157)
- [github.com/RodneyShag](https://github.com/RodneyShag)
