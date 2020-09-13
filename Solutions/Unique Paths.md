### Algorithm

We can solve this problem mathematically using the "Combinations" formula:

- Let x = number of moves to go from left side of grid to right side of grid
- Let y = number of moves to go from top of grid to bottom of grid (assuming no obstacles)

```
 (x + y)!  
 --------
 (x!)(y!)
```

- There are (x+y) moves total. Choose x of them to go right, (and the remaining y moves will pick themselves)

Example: For a 3x3 maze, we get x = 2, y = 2. Our formula gives (2+2)!((2!)(2!)) = 6.

### Efficient calculation

Instead of calculating the above formula directly, we can cancel factors before calculating the product. For example:

```
 (5 + 3)!       8*7*6*5*4*3*2*1     8*7*6
 --------  =  ------------------ =  -----
 (5!)(3!)     (5*4*3*2*1)(3*2*1)    3*2*1
```

The code below shows implements this approach

### Solution

```java
class Solution {
    public int uniquePaths(int m, int n) throws IllegalArgumentException {
        if (m > n) {
            return uniquePaths(n, m); // so that 1st argument is smaller, to improve runtime.
        }
        if (m < 1 || n < 1) {
            throw new IllegalArgumentException();
        }

        int downSteps = m - 1;
        int rightSteps = n - 1;
        int totalSteps = downSteps + rightSteps;

        long product = 1; // use long instead of int to avoid integer overflow
        int numBot = 1;
        for (int numTop = rightSteps + 1; numTop <= totalSteps; numTop++, numBot++) {
            product *= numTop;
            product /= numBot;
        }
        return (int) product;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(min(m + n))
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
