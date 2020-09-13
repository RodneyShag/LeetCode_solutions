### Algorithm

- This is the same problem as [Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1), but with Duplicates allowed.
- Use [this solution](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Insert%20Delete%20GetRandom%20O%281%29.md) and replace the `Map<Integer, Integer>` with a `Map<Integer, LinkedHashSet<Integer>>`, where the `LinkedHashSet` will represent all the indices of a given number.
    - We use a `LinkedHashSet` instead of a `HashSet` since `.next()` on a `LinkedHashSet` will be O(1) time.
        - "Iteration over a `LinkedHashSet` requires time proportional to the _size of the set_, regardless of its capacity. Iteration over a `HashSet` is likely to be more expensive, requiring time proportional to its _capacity_" ([Reference](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashSet.html)).

### Solution

```java
class RandomizedCollection {
    Random rand = new Random();
    List<Integer> list = new ArrayList();
    Map<Integer, LinkedHashSet<Integer>> valToIndices = new HashMap();

    public boolean insert(int num) {
        // update Map
        if (!valToIndices.containsKey(num)) {
            valToIndices.put(num, new LinkedHashSet());
        }
        valToIndices.get(num).add(list.size());

        // update List
        list.add(num);

        return valToIndices.get(num).size() == 1;
    }

    public boolean remove(int num) {
        if (!valToIndices.containsKey(num) || valToIndices.get(num).isEmpty()) {
            return false;
        }

        int indexToRemove = valToIndices.get(num).iterator().next();
        int valueLast = list.get(list.size() - 1);

        // update List
        list.set(indexToRemove, valueLast);
        list.remove(list.size() - 1);

        // update Map: remove overwritten index from set
        valToIndices.get(num).remove(indexToRemove);

        // update Map: update the moved number's index
        valToIndices.get(valueLast).add(indexToRemove);                              
        valToIndices.get(valueLast).remove(list.size());

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
    return valToIndices.containsKey(num) && !valToIndices.get(num).isEmpty();
}
```

### Time/Space Complexity

- Time Complexity: `O(1)` for insert(), remove(), getRandom(), contains(). Technically it's "amortized O(1)" time, since that's the runtime for adding to `ArrayList` or `HashMap` in Java.
- Space Complexity: `O(1)` for each added element

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
