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

### Additional Notes

Using AND and XOR operators is literally how addition is done in circuits, using a [Half Adder](https://en.wikipedia.org/wiki/Adder_%28electronics%29#Half_adder)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/sum-of-two-integers/discuss/308122)
- [github.com/RodneyShag](https://github.com/RodneyShag)
