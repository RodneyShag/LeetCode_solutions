### List of Solutions

| # |           Solutions            | Runtime |   Space   |  Preference  |
|:-:|:------------------------------:|:-------:|:---------:|:------------:|
| 1 | Dynamic Programming: Recursive |   O(n)  |   O(n)    |       -      |
| 2 | Dynamic Programming: Iterative |   O(n)  |   O(n)    |       -      |
| 3 | Iterative, no array            |   O(n)  |   O(1)    |   Favorite   |

### Notes

Our input `n` guaranteed to be a positive integer (1, 2, 3,...)

### Solution 1 - Dynamic Programming: Recursive

```java
class Solution {
    public int climbStairs(int n) {
        int[] cache = new int[n + 1];
        return climbStairs(n, cache);
    }

    private int climbStairs(int n, int[] cache) {
        if (n < 0) { // this can happen due to our recursive calls
            return 0;
        } else if (n == 0 || n == 1) {
            return 1;
        }
        if (cache[n] > 0) {
            return cache[n];
        }
        cache[n] = climbStairs(n - 1, cache)
                 + climbStairs(n - 2, cache);

        return cache[n];
    }
}
```

### Solution 2 - Dynamic Programming: Iterative

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }
        int[] cache = new int[n + 1];
        cache[0] = 1;
        cache[1] = 1;
        for (int i = 2; i <= n; i++) {
            cache[i] = cache[i - 2] + cache[i - 1];
        }
        return cache[n];
    }
}
```

### Solution 3 - Iterative, no array

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }
        int prev = 1;
        int curr = 1;
        int next = 0;
        for (int i = 2; i <= n; i++) {
            next = prev + curr;
            prev = curr;
            curr = next;
        }
        return curr;
    }
}
```

### Additional Notes

[According to LeetCode Solutions 5 and 6](https://leetcode.com/problems/climbing-stairs/solution), this problem can also be solved in log(n) time using either Matrix Multiplication, or the Fibonacci formula. However, those solutions are out of scope for a coding interview, as they are too mathematical.
