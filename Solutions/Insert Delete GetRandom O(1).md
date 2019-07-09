### Algorithm

1. If we had an array, we could get a random element in it in O(1) time.
    - For example, if the array had `n` elements in it, we would generate a random integer from [0,n) and return the value at that index.
1. Maintain 2 data structures to represent our `RandomizedSet`
    - __array__: Use an array (or `ArrayList`) to store the actual elements. Use the logic above to get a random element in O(1) time.
    - __Map__: Our array gave "index-to-value". This `Map` will store "value-to-index" of the array elements. This lets us see if an element exists in our `RandomizedSet` in O(1) time.
1. Item removal
    - __array__: When removing an item from our `RandomizedSet`, we may have a hole in our array. We can fill in the hole by moving the last element in our array into that position.
    - __Map__: Since last item in list was moved, update `Map` to reflect this change in position.

### Solution

```java
class RandomizedSet {
    Random rand = new Random();
    List<Integer> list = new ArrayList<>();
    Map<Integer, Integer> valToInd = new HashMap<>();

    public boolean insert(int num) {
        if (valToInd.containsKey(num)) {
            return false;
        }
        valToInd.put(num, list.size());
        list.add(num);
        return true;
    }

    public boolean remove(int num) {
        if (!valToInd.containsKey(num)) {
            return false;
        }

        int indexToRemove = valToInd.get(num);
        int valueLast = list.get(list.size() - 1);

        // update List
        list.set(indexToRemove, valueLast);
        list.remove(list.size() - 1);

        // update Map
        valToInd.put(valueLast, indexToRemove);
        valToInd.remove(num);

        return true;
    }

    public int getRandom() { // will fail if set is empty.
        int index = rand.nextInt(list.size());
        return list.get(index);
    }
}
```

### Implementation Details

In the code above, where we " update Map: update the moved number's index", we must do the `put` before the `remove`. This is to pass test cases like "add 7" then "remove 7". In this scenario, we want to ensure our `Set<Integer>` (for value 7) ends up empty.

### Additional functionality

The problem could be improved by asking for O(1) time for checking our Set for a value:

```java
public boolean contains(int num) {
  return valToInd.containsKey(num);
}
```

### Time/Space Complexity

- Time Complexity: `O(1)` for insert(), remove(), getRandom(), contains(). Technically it's "amortized O(1)" time, since that's the runtime for adding to `ArrayList` or `HashMap` in Java.
- Space Complexity: `O(1)` for each added element
