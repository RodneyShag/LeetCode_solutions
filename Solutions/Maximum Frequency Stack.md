### Algorithm

__Saving frequency of each number__ - Create `Map<Integer, Integer> freq` that's a `Map` from `x` to the number of occurrences of `x`.

__Saving highest frequencies in descending order__ - Create `Map<Integer, Stack<Integer>> stacks` which is a `Map` from frequency (1, 2,...) to a `Stack` of `Integers` with that frequency. For example, if `53` is pushed twice, the first copy will be saved to Stack 1, the second copy to Stack 2.

We use `Stack`s so that "if there is a tie for most frequent element, the element closest to the top of the stack is removed and returned."

Keep track of `maxFreq` which is basically a pointer to the largest key in `stacks`.

`push()` and `pop()` are implemented by updating the above `freq`, `stacks`, and `maxFreq`.

[Alternative explanation](https://leetcode.com/articles/maximum-frequency-stack/)

### Example

Example showing how `Map<Integer, Stack<Integer>> stacks` is updated:

```
// push(5) gives
Stack 1 = [5]  // maxFreq = 1
Stack 2 = []

// push(4) gives
Stack 1 = [5, 4]  // maxFreq = 1
Stack 2 = []

// push(5) gives
Stack 1 = [5, 4]
Stack 2 = [5]     // maxFreq = 2

// pop(5) gives
Stack 1 = [5, 4]  // maxFreq = 1
Stack 2 = []

```
### Solution

```java
class FreqStack {
    private Map<Integer, Integer> freq = new HashMap();
    private Map<Integer, Stack<Integer>> stacks = new HashMap();
    private int maxFreq = 0;

    public void push(int x) {
        freq.merge(x, 1, Integer::sum);
        int f = freq.get(x);
        maxFreq = Math.max(maxFreq, f);
        stacks.putIfAbsent(f, new Stack());
        stacks.get(f).add(x);
    }

    public int pop() {
        int x = stacks.get(maxFreq).pop();
        freq.merge(x, -1, Integer::sum);
        if (stacks.get(maxFreq).isEmpty()) {
            maxFreq--;
        }
        return x;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(1) for push and pop
- Space Complexity: O(1) for storage of each element. Can alternatively describe it as O(n) for storage of n elements.
