### Algorithm

- `stack1` will accept input elements for `push()`
- `stack2` will output elements for `pop()`, `peek()`
- when trying to do a `pop()` or `peek()` on our queue, if `stack2` is empty, we will move all elements from `stack1` to `stack2`. This will reverse the order of the elements, giving us the correct order when we call `pop()` or `peek()` on our queue.

### Solution

```java
class MyQueue {
    private Stack<Integer> stack1 = new Stack<>();
    private Stack<Integer> stack2 = new Stack<>();

    public void push(int x) {
        stack1.push(x);
    }

    public int pop() {
        if (stack2.isEmpty()) {
            shiftStacks();
        }
        return stack2.pop();
    }

    public int peek() {
        if (stack2.isEmpty()) {
            shiftStacks();
        }
        return stack2.peek();
    }

    public boolean empty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }

    private void shiftStacks() {
        while (!stack1.isEmpty()) {
            int temp = stack1.pop();
            stack2.push(temp);
        }
    }
}
```

### Implementation Notes

- LeetCode problem statement says it will not perform invalid operations such as `peek()` or `pop()` on an empty stack. A more general solution should check for an empty queue in `peek()` and `pop()`, and if the queue is empty, either:
  1. throw an error
  1. return null (which would require changing the return value from `int` to `Integer`)
- `add()` is a better name than `push()` for a queue.
- `remove()` is a better name than `pop()` for a queue.

### Time/Space Complexity

-  Time Complexity: O(1) _amortized_ time for `push()`, `pop()`, `peek()`, `empty()`, as each element is only moved from `stack1` to `stack2` at most once.
- Space Complexity: O(1) for each element being put into our queue.
