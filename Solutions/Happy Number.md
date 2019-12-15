### Algorithm

This is similar to [LeetCode #141 - Linked List Cycle](https://leetcode.com/problems/linked-list-cycle). We will reuse the [algorithm from that problem](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Linked%20List%20Cycle.md) to detect cycles.

1. Create `slow`. It will move 1 step  at a time.
1. Create `fast`. It will move 2 steps at a time.
1. We will keep generating numbers until either
    1. We generate `1` (we have a "happy number"), or
    1. `slow` and `fast` collide (we don't have a "happy number").

### Solution

```java
class Solution {
    public boolean isHappy(int n) {
        if (n <= 0) {
            return false;
        }
        int slow = n;
        int fast = digitSquareSum(n);  // setting fast to n would cause an immediate `slow == fast` collision

        while (fast != 1 && slow != fast) {
            slow = digitSquareSum(slow);
            fast = digitSquareSum(fast);
            fast = digitSquareSum(fast);
        }

        return fast == 1;
    }

    private int digitSquareSum(int n) {
        int sum = 0;
        while (n > 0) {
            int digit = n % 10;
            sum += digit * digit;
            n /= 10;
        }
        return sum;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/happy-number/discuss/451908)
- [github.com/RodneyShag](https://github.com/RodneyShag)
