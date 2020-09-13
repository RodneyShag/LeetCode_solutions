### Explanation

Assuming it's your turn, here are the base cases solved:

```
1 stone --> Win. Take 1 stone.
2 stones --> Win. Take 2 stones.
3 stones --> Win. Take 3 stones.
4 stones --> Lose. If you take 1, 2, or 3 stones, your opponent will take the remaining stones.
5 stones --> Win. Take 1 stone, and your opponent is left with the losing 4 stone situation.
6 stones --> Win. Take 2 stones, and your opponent is left with the losing 4 stone situation.
7 stones --> Win. Take 3 stones, and your opponent is left with the losing 4 stone situation.
8 stones --> Lose. If you take 1, 2, or 3 stones, your opponent can take enough stones to leave you with the 4 stone losing situation.
```

This pattern repeats, where every multiple of 4 is a losing situation if it is your turn to play.

### Solution

```java
class Solution {
    public boolean canWinNim(int n) {
        return n % 4 != 0;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
