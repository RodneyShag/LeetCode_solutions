# Solution 1 - Using `long`

### Notes

An `int` is 32 bits, so we can use a `long` to prevent integer overflow.

### Code

```java
class Solution {
    public int reverse(int x) {
        long rev = 0;
        while (x != 0) {
            rev = 10 * rev + x % 10;
            x = x / 10;
        }
        return rev > Integer.MAX_VALUE || rev < Integer.MIN_VALUE
               ? 0
               : (int) rev;
    }
}
```

### Examples

Input: 19

```
    Initial: rev =  0, x = 19
Iteration 1: rev =  9, x =  1
Iteration 2: rev = 91, x =  0
```

Input: -19

```
    Initial: rev =   0, x = -19
Iteration 1: rev =  -9, x =  -1
Iteration 2: rev = -91, x =   0
```

The tricky part for negative numbers is that `-19 % 10 = -9`

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)


# Solution 2 - Using a Math Trick

### Notes

- The line `rev = 10 * rev + x % 10;` may cause overflow.
- After executing the above line, we can immediately undo this line by running `(rev - x % 10) / 10`. If this doesn't give us our previous result of `rev`, we have overflow.

### Code

```java
class Solution {
    public int reverse(int x) {
        int prevRev = 0;
        int rev = 0;
        while (x != 0) {
            rev = 10 * rev + x % 10;
            if ((rev - x % 10) / 10 != prevRev) { // check overflow
                return 0;
            }
            prevRev = rev;
            x = x / 10;
        }
        return rev;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)


# Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
