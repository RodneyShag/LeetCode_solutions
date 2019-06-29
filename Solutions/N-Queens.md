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
    public List<List<String>> solveNQueens(int n) {
        if (n < 0) {
            return 0;
        }
        char[][] board = new char[n][n];
        for (char[] row : board) {
            Arrays.fill(row, '.');
        }
        Set<Integer> cols = new HashSet<>(); // columns   |
        Set<Integer> d1 = new HashSet<>();   // diagonals \
        Set<Integer> d2 = new HashSet<>();   // diagonals /

        List<List<String>> solutions = new ArrayList<>();
        placeQueens(board, n, solutions, 0, cols, d1, d2);
        return solutions;
    }

    private void placeQueens(char[][] board, int n, List<List<String>> solutions, int row,
                             Set<Integer> cols, Set<Integer> d1, Set<Integer> d2) {
        if (row == n) {
            solutions.add(makeSolutionBoard(board));
            return;
        }
        for (int col = 0; col < n; col++) {
            int diag1 = col - row;
            int diag2 = col + row;
            if (cols.contains(col) || d1.contains(diag1) || d2.contains(diag2)) {
                continue;
            }
            // put queen on board
            board[row][col] = 'Q';
            cols.add(col);
            d1.add(diag1);
            d2.add(diag2);

            placeQueens(board, n, solutions, row + 1, cols, d1, d2);

            // remove queen from board
            cols.remove(col);
            d1.remove(diag1);
            d2.remove(diag2);
            board[row][col] = '.';
        }
    }

    private List<String> makeSolutionBoard(char[][] board) {
        List<String> solution = new ArrayList<>();
        for (char[] row : board) {
            solution.add(new String(row));
        }
        return solution;
    }
}
```

### Time Complexity

Time Complexity: O(n!) due to the size of our recursion tree


- We used recursion to brute-force traverse this tree, trying every possible queen combination (other than the combinations that immediately fail). We never place a queen on the same column as a previous queen, which is why the number of choices on each row is 8, then at most 7, then at most 6, ... down to at most 1.
- Our Recursion Tree will have n + 1 = 9 levels in it
  - Our root will have 1 node in it.
  - Our next level represents row 0 (and will have 8 nodes in it)
  - Our next level represents row 1 (and will have 8 x 7 = 56 nodes in it)
  - Our last level represents row 7 (and will have 8 x 7 x 6... = 8! nodes in it)
  - Therefore our recursion tree is of size O(n!) (which is determined by the n! leaves in the tree)

### Space Complexity

If every leaf in our recursion tree represented a solution, our space complexity would be O(n!). However, for an 8x8 board, there are only exactly 92 solutions.

It might make more sense to represent our space complexity as O(d * n<sup>2</sup>) where `d` is the number of solution boards. Keep in mind that `d` is not a constant, and also grows as `n` grows.
