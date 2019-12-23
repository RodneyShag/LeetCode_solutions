### Algorithm

- The elements of the `kth` row of Pascal's triangle are equal to the coefficients of the expansion of (a + b)<sup>k</sup>
- For the 4th line, `k = 4`, so we have (a + b)<sup>4</sup> = a<sup>4</sup> + 4a<sup>3</sup>b + 6a<sup>2</sup>b<sup>2</sup> + 4ab<sup>3</sup> + b<sup>4</sup>
- The coefficients of the above polymonial are `1 4 6 4 1`, which is the same as the 4th row of Pascal's triangle
- These coefficients could be calculated directly as <sub>4</sub>C<sub>0</sub>, <sub>4</sub>C<sub>1</sub>, <sub>4</sub>C<sub>2</sub>, <sub>4</sub>C<sub>3</sub>, <sub>4</sub>C<sub>4</sub>, using the [Combination Formula](https://www.mathwords.com/c/combination_formula.htm) which lets us [calculate any number in Pascal's triangle directly](https://www.mathwords.com/b/binomial_coefficients_pascal.htm)
- As an optimization, we can reuse the previous number in a row to create the next number. [This is how you calculate the numbers in the kth row](https://math.stackexchange.com/a/1154968).

### Solution

```java
class Solution {
    public List<Integer> getRow(int k) {
        if (k < 0) {
            return new ArrayList();
        }
        List<Integer> row = new ArrayList();
        row.add(1);
        int top = k; // multiplier in numerator
        int bot = 1; // multiplier in denominator
        long C = 1; // use a `long` to prevent integer overflow
        for (int i = 1; i <= k; i++) {
            C *= top;
            C /= bot;
            top--;
            bot++;
            row.add((int) C);
        }
        return row;
    }
}
```

which can be simplified to:

```java
class Solution {
    public List<Integer> getRow(int k) {
        if (k < 0) {
            return new ArrayList();
        }
        List<Integer> row = new ArrayList();
        row.add(1);
        long C = 1; // use a `long` to prevent integer overflow
        for (int i = 1; i <= k; i++) {
            C = C * (k + 1 - i) / i;
            row.add((int) C);
        }
        return row;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(k)
- Space Complexity: O(k)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/pascals-triangle-ii/discuss/458235)
- [github.com/RodneyShag](https://github.com/RodneyShag)
