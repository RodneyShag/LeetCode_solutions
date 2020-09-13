### Notes

uses XOR. Keep in mind:

1. x ^ x = 0
1. x ^ 0 = x
1. XOR is commutative and associative

### Solution

```java
class Solution {
    public int singleNumber(int[] array) {
        int result = 0;
        for (int num : array) {
            result = result ^ num; // ^ is XOR operator
        }
        return result;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
