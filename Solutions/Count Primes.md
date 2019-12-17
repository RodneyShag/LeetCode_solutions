### Algorithm

This algorithm is called [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

![Sieve of Eratosthenes](images/sieveOfEratosthenes.gif)

1. Create `boolean[] flags` where each `true` represents a prime number.
    - Initialize all numbers 2 and bigger as `true` for now, we will later cross off the non-prime numbers.
1. Start at prime number 2 and cross off all multiples of 2. Repeat this step for the remaining prime numbers.

### Optimization 1

Notice we only need to loop to square root of n (instead of n) to cross off all non-primes

### Optimization 2

To cross off multiples of prime `p`, we want to cross off `2p`, `3p`, `4p`, `5p`, but all `kp` where `k < p` have already been crossed off in a previous step. For this reason, for each prime, we can start crossing off at `p * p`


### Solution

```java
class Solution {
    public int countPrimes(int n) {
        if (n < 2) {
            return 0;
        }
        boolean[] isPrime = new boolean[n];
        for (int i = 2; i < n; i++) {
            isPrime[i] = true;
        }

        int sqrt = (int) Math.sqrt(n);
        for (int p = 2; p <= sqrt; p++) {
            if (isPrime[p]) {
                for (int i = p * p; i < n; i += p) {
                    isPrime[i] = false;
                }
            }
        }

        int count = 0;
        for (int i = 2; i < n; i++) {
            if (isPrime[i]) {
                count++;
            }
        }
        return count;
    }
}
```

### Time Complexity

Since we have nested loops, our runtime is `O(sqrt(n) * n)`.

However, this analysis did not take into account that the inner loop is skipped whenever `isPrime[i]` is true. The actual time complexity is `O(n * log(log(n)))` according to [this link](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes#Algorithmic_complexity), but understanding/explaining it during an interview is definitely not expected.

### Space Complexity

O(n) due to `boolean[] isPrime`

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/count-primes/discuss/452628)
- [github.com/RodneyShag](https://github.com/RodneyShag)
