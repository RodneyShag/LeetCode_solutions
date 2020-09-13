### Algorithm

Use `Semaphore`s to represent `H` and `O`. Here is a good explanation of [Semaphores](https://www.geeksforgeeks.org/semaphore-in-java/) (read their explanation, skip their code).

We can use a [CyclicBarrier](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CyclicBarrier.html#await--) to create a barrier for every 3 elements. However, `CyclicBarrier` can throw a `BrokenBarrierException` when calling `await()`, so we instead use a [Phaser](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Phaser.html) to avoid having to catch or throw  `BrokenBarrierException`.  We use this `Phaser` to wait for 3 elements to form a molecule, before releasing another 2 `H` and 1 `O` elements.

The problem statement is unclear whether there are 2 threads or 3 threads of `H20` class running. The code below assumes we have 3 threads of `H20` running simultaneously.

### Solution

```java
class H2O {
    private Semaphore semH = new Semaphore(2);
    private Semaphore semO = new Semaphore(1);
    private Phaser phaser = new Phaser(3);

    public void hydrogen(Runnable releaseHydrogen) throws InterruptedException {
		semH.acquire();
        releaseHydrogen.run(); // outputs "H"
        phaser.arriveAndAwaitAdvance();
        semH.release();
    }

    public void oxygen(Runnable releaseOxygen) throws InterruptedException {
        semO.acquire();
		releaseOxygen.run(); // outputs "O"
        phaser.arriveAndAwaitAdvance();
        semO.release();
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) since string will have O(n) characters
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
