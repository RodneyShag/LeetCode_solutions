### Algorithm

Use Semaphores. Here is a good explanation of [Semaphores](https://www.geeksforgeeks.org/semaphore-in-java/) (read their explanation, skip their code).

- use `Semaphore fooLock` to block execution of `foo()`
- use `Semaphore barLock` to block execution of `bar()`
- `fooLock` will start unlocked so that `foo()` is first function to execute.

### Solution

```java
class FooBar {
    private int n;
    private Semaphore fooLock = new Semaphore(1);
    private Semaphore barLock = new Semaphore(0);

    public FooBar(int n) {
        this.n = n;
    }

    public void foo(Runnable printFoo) throws InterruptedException {
        for (int i = 0; i < n; i++) {
            fooLock.acquire();
        	printFoo.run();
            barLock.release();
        }
    }

    public void bar(Runnable printBar) throws InterruptedException {        
        for (int i = 0; i < n; i++) {
            barLock.acquire();
        	printBar.run();
            fooLock.release();
        }
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/print-foobar-alternately/discuss/392077)
- [github.com/RodneyShag](https://github.com/RodneyShag)
