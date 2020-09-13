### Assumptions

Since problem statement isn't clear on what to do when our stack is empty, we have to make the following assumptions:

1. `top()` will never be called on an empty stack
1. `getMin()` will never be called on an empty stack

### Solution

```java
class MinStack {
    Stack<Integer> stack = new Stack();
    Stack<Integer> minStack = new Stack(); // keeps track of minimums

    // Always push onto stack. If it's a minimum, also push it onto minStack
    public void push(int x) {
        stack.push(x);
        if (minStack.isEmpty() || x <= getMin()) {
            minStack.push(x);
        }
    }

    // Pop off stack. If we popped a minimum, we remove it from minStack also
    public void pop() {
        if (stack.isEmpty()) {
            return;
        }
        int x = stack.pop();
        if (x == minStack.peek()) {
            minStack.pop();
        }
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(1) for `push()`, `pop()`, `top()`, and `getMin()`
- Space Complexity: O(n) to store n `Integer`s

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
