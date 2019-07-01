# Solution 1 - Recursive

### Algorithm

Try all possibilities. Whenever we conclude that a certain array index has no solution, mark it by setting it's value to 0.

### Code

```java
class Solution {
    public boolean canJump(int[] array) {
        if (array == null || array.length == 0) {
            return false;
        }
        return canJump(array, 0);
    }

    private boolean canJump(int[] array, int i) {
        // Base Cases
        if (i == array.length - 1) {
            return true;
        } else if (i < 0 || i >= array.length || array[i] == 0) {
            return false;
        }

        // Recursive Cases
        for (int jumpSize = 1; jumpSize <= array[i]; jumpSize++) {
            if (canJump(array, i + jumpSize)) {
                return true;
            }
        }

        array[i] = 0; // marks as visited
        return false;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n) since we mark elements as visited
- Space Complexity: O(n) due to recursion

# Solution 2 - Iterative

### Algorithm

1. Iterate left-to-right through the array.
1. For each index `i` in the array, see what the maximum jump `reach` you have.
1. As long as there are elements within `reach` that we haven't tried, keep going until you reach the end of the array. If we get to end, `return true`. If not, `return false`.

### Code

```java
class Solution {
    public boolean canJump(int[] array) {
        int reach = 0;
        for (int i = 0; i <= reach; i++) {
            reach = Math.max(reach, i + array[i]);
            if (reach >= array.length - 1) {
                return true;
            }
        }
        return false;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

Due to our jump value being [0, jump], we can solve this in O(1) space. However, this O(1) space solution is not possible in all variations to this problem, such as [this problem](https://github.com/RodneyShag/Interview_solutions/blob/master/Questions/HackerRank/Java%201D%20Array.md).
