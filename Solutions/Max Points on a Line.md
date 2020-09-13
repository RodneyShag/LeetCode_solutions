### Algorithm

- To find max number of points on same line, we can find most popular line by drawing a line between every pair of points.
- Can represent a line as a "slope" of (y2 - y1)/(x2 - x1), and see how many lines have the same slope.
- We want to use a HashMap<Double, Integer> where
    - key is slope
    - value is number of lines with that slope
- However, we can't use a Double as a key in a HashMap due to precision problems with ==.
- Fortunately, our input uses int and not double, so we can create a hash key using: `String slope = y + "/" + x` where we use GCD to put the slope in lowest terms.
- Example: y/x = 8/6 = 4/3 since GCD of x,y is 2.

### Solution

```java
class Solution {
    public int maxPoints(int[][] points) {
        if (points == null) {
            return 0;
        } else if (points.length <= 2) {
            return points.length;
        }
        int solution = 0;
        for (int i = 0; i < points.length - 1; i++) {
            // find max number of points that lie on same line, starting at points[i]
            Map<String, Integer> map = new HashMap();
            int samePoint = 0;
            for (int j = i + 1; j < points.length; j++) {
                int x = points[i][0] - points[j][0];
                int y = points[i][1] - points[j][1];
                if (x == 0 && y == 0) {
                    samePoint++;
                    continue;
                }
                int gcd = generateGcd(x, y);
                x /= gcd;
                y /= gcd;
                String slope = y + "/" + x; // key for HashMap
                map.merge(slope, 1, Integer::sum);
            }

            int linesMax = 0;
            for (int value : map.values()) {
                linesMax = Math.max(linesMax, value);
            }

            solution = Math.max(solution, 1 + linesMax + samePoint);
        }
        return solution;
    }

    private int generateGcd(int a, int b) { // Euclid's Greatest Common Divisor (GCD) Algorithm
        while (b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n^2)
- Space Complexity: O(n) due to HashMap

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
