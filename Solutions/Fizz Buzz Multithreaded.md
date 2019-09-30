### Algorithm

- We have 4 threads running simultaneously.
- `num` will start at `1`, and will be incremented to `n`.
- Each thread checks `num` to see if it should take its turn
    - __If__ thread should print, then
        1. print
        1. increment `num`
        1. wake up all waiting threads
    - __Else__, [wait()](https://www.baeldung.com/java-wait-and-sleep) on this thread until another thread processes `num`. Once 1 of the 4 threads processes `num`, that thread will call `notifyAll()` to wake up all 4 threads.

The `while (num <= n)` is in the code to ensure each thread has the current number `num` in valid range `[1 to n]` to process.

### Solution

```java
class FizzBuzz {
    private int n;
    private int num = 1;

    public FizzBuzz(int n) {
        this.n = n;
    }

    public synchronized void fizzbuzz(Runnable printFizzBuzz) throws InterruptedException {
        while (num <= n) {
            if (num % 15 == 0) {
                printFizzBuzz.run();
                num++;
                notifyAll();
            } else {
                wait();
            }
        }
    }

    public synchronized void fizz(Runnable printFizz) throws InterruptedException {
        while (num <= n) {
            if (num % 3 == 0 && num % 5 != 0) {
                printFizz.run();
                num++;
                notifyAll();
            } else {
                wait();
            }
        }
    }

    public synchronized void buzz(Runnable printBuzz) throws InterruptedException {
        while (num <= n) {
            if (num % 3 != 0 && num % 5 == 0) {
                printBuzz.run();
                num++;
                notifyAll();
            } else {
                wait();
            }
        }
    }

    public synchronized void number(IntConsumer printNumber) throws InterruptedException {
        while (num <= n) {
            if (num % 3 != 0 && num % 5 != 0) {
                printNumber.accept(num);
                num++;
                notifyAll();
            } else {
                wait();
            }
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)
