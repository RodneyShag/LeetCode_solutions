### Hint

Visualize the triangle in the shape shown below, so when we access it using `i` (for row) and `j` (for column), it is simpler to see which number we're accessing

```
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
```

For example, `i = 4` and `j = 2` gives us value `4`

### Solution

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        if (numRows <= 0) {
            return new ArrayList();
        }
        List<List<Integer>> triangle = new ArrayList();
        triangle.add(Arrays.asList(1)); // Row 0
        for (int i = 1; i < numRows; i++) {
            List<Integer> prevRow = triangle.get(i - 1);
            List<Integer> row = new ArrayList();
            row.add(1);
            for (int j = 1; j < i; j++) {
                row.add(prevRow.get(j - 1) + prevRow.get(j));
            }
            row.add(1);
            triangle.add(row);
        }
        return triangle;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(n<sup>2</sup>)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
