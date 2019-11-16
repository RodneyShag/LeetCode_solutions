### Notes

This solution is a simplification of the [general N-Queens problem](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/N-Queens.md)

### Algorithm

Use "Backtracking" - an algorithm for finding all solutions by exploring all potential candidates.

We will keep track of:
  1. Which columns we've already placed a queen in
  1. Which diagonals (top-left to bottom-right) we've placed a queen in
  1. Which diagonals (top-right to bottom-left) we've placed a queen in

```
Let's number the diagonals (in the direction of a backslash \)

The numbers at the left of the grid are the rows.
The numbers at the top of the grid are the cols.
The numbers in the cells are generated using the formula: : col - row

for a 3x3 chess board, we have:

     0    1    2
  ----------------
0 |  0 |  1 |  2 |
1 | -1 |  0 |  1 |
2 | -2 | -1 |  0 |
  ----------------

For example, the cell [0][0], and the cell [2][2] will have the same value using the formula.
```

```
Let's number the diagonals (in the direction of a forward-slash /)
The numbers in the cells are generated using the formula: col + row

for a 3x3 chess board, we have:

    0   1   2
  -------------
0 | 0 | 1 | 2 |
1 | 1 | 2 | 3 |
2 | 2 | 3 | 4 |
  -------------

For example, the cell [2][0], and the cell [0][2] will have the same value using the formula.
```

### Solution

```java
class Solution {
    private int count;

    public int totalNQueens(int n) {
        if (n < 0) {
            return 0;
        }
        Set<Integer> cols = new HashSet<>(); // columns   |
        Set<Integer>   d1 = new HashSet<>(); // diagonals \
        Set<Integer>   d2 = new HashSet<>(); // diagonals /
        placeQueens(n, 0, cols, d1, d2);
        return count;
    }

    private void placeQueens(int n, int row, Set<Integer> cols, Set<Integer> d1, Set<Integer> d2) {
        if (row == n) {
            count++;
            return;
        }
        for (int col = 0; col < n; col++) {
            int diag1 = col - row;
            int diag2 = col + row;
            if (cols.contains(col) || d1.contains(diag1) || d2.contains(diag2)) {
                continue;
            }
            // put queen on board
            cols.add(col);
            d1.add(diag1);
            d2.add(diag2);

            placeQueens(n, row + 1, cols, d1, d2);

            // remove queen from board
            cols.remove(col);
            d1.remove(diag1);
            d2.remove(diag2);
        }
    }
}
```

### Time Complexity

Time Complexity: `O(n!)` due to the size of our recursion tree

- We used recursion to brute-force traverse this tree, trying every possible queen combination (other than the combinations that immediately fail). We never place a queen on the same column as a previous queen, which is why the number of choices on each row is 8, then at most 7, then at most 6, ... down to at most 1.
- Our Recursion Tree will have n + 1 = 9 levels in it
  - Our root will have 1 node in it.
  - Our next level represents row 0 (and will have 8 nodes in it)
  - Our next level represents row 1 (and will have 8 x 7 = 56 nodes in it)
  - Our last level represents row 7 (and will have 8 x 7 x 6... = 8! nodes in it)
  - Therefore our recursion tree is of size O(n!) (which is determined by the n! leaves in the tree)

### Space Complexity

O(n), as that is the maximum depth of our recursion, and is also the size of each `HashSet` we use.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/n-queens-ii/discuss/309039)
- [github.com/RodneyShag](https://github.com/RodneyShag)
