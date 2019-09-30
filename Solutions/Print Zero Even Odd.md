### Hints

Use Semaphores. Here is a good explanation of [Semaphores](https://www.geeksforgeeks.org/semaphore-in-java/) (read their explanation, skip their code).

### Solution

```java
class ZeroEvenOdd {
    private int n;
    Semaphore zeroLock = new Semaphore(1);
    Semaphore  oddLock = new Semaphore(0);
    Semaphore evenLock = new Semaphore(0);

    public ZeroEvenOdd(int n) {
        this.n = n;
    }

    public void zero(IntConsumer printNumber) throws InterruptedException {
        for (int i = 0; i < n; i++) {
            zeroLock.acquire();
        	printNumber.accept(0);
            if (i % 2 == 0) {
                oddLock.release();
            } else {
                evenLock.release();
            }

        }
    }

    public void even(IntConsumer printNumber) throws InterruptedException {
        for (int i = 2; i <= n; i += 2) {
            evenLock.acquire();
        	printNumber.accept(i);
            zeroLock.release();
        }
    }

    public void odd(IntConsumer printNumber) throws InterruptedException {
        for (int i = 1; i <= n; i += 2) {
            oddLock.acquire();
        	printNumber.accept(i);
            zeroLock.release();
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)
