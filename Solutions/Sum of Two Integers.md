### Algorithm

- We can represent addition by using the AND operator (`&`) and XOR (`^`) operator.
- AND will give us the 'carry', and XOR will give us the 'sum'. The 'carry' and 'sum' together will give us our result.
- This solution works for negative numbers as well.

### Solution

```java
class Solution {
    public int getSum(int a, int b) {
        if (b == 0) {
            return a;
        }
        int sum = a ^ b;
        int carry = (a & b) << 1;
        return getSum(sum, carry);
    }
}
```

### Example

```
a = 001
b = 011

       a ^ b = 010  // 'sum'
(a & b) << 1 = 010  // 'carry'
```

```
Now we add the 'sum' (shown as 'a') and 'carry' (shown as 'b')

a = 010
b = 010

       a ^ b = 000  // 'sum'
(a & b) << 1 = 100  // 'carry'
```

```
Again, we add 'sum' and 'carry'

       a ^ b = 100  // 'sum'
(a & b) << 1 = 000  // 'carry'

Now that we no longer have a carry, our algorithm finishes, and we return 'sum' of 100
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

### Time/Space Complexity for # of bits

- The above complexities are O(1) since we are dealing with 32-bit `int`s in Java, so the # of times we add `carry` and `sum` is always a max of 32.
- If we want to be fancy and let `n = # of bits in each number`, with no restriction on the number of bits in a number, then we would have
  -  Time Complexity: O(n) due to O(n) recursive calls
  - Space Complexity: O(n) due to O(n) recursive calls


- There is also an [iterative solution](https://leetcode.com/problems/sum-of-two-integers/discuss/132479/Simple-explanation-on-how-to-arrive-at-the-solution) that exists for this problem. However, there is no improvement in runtime or space complexity when using the iterative solution
    - Although our recursive solution makes O(n) recursive calls, where `n = # of bits in each number`, any iterative solution that creates a new `int` would require O(n) space for storage of the additional `int` (for example, when calculating `a ^ b`)


### Additional Notes

Using AND and XOR operators is literally how addition is done in circuits, using a [Half Adder](https://en.wikipedia.org/wiki/Adder_%28electronics%29#Half_adder)
