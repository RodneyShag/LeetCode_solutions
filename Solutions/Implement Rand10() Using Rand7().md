### Algorithm

- We are provided a function `rand7()` generates a random number from 1 to 7 inclusive, so `rand7() -1` generates a random number from 0 to 6 inclusive.
- Our formula: `7 * (rand7() - 1) + (rand7() - 1)` will generate a random number from 0 to 48 inclusive, where all numbers will be evenly distributed
  - The `7 * (rand7() - 1)` represents the row (in table below)
  - The `(rand7() - 1)` represents the column (in table below)

```
       0    1    2    3    4    5    6
    ----------------------------------
0  |   0    1    2    3    4    5    6
1  |   7    8    9   10   11   12   13
2  |  14   15   16   17   18   19   20
3  |  21   22   23   24   25   26   27
4  |  28   29   30   31   32   33   34
5  |  35   36   37   38   39   40   41
6  |  42   43   44   45   46   47   48
```

We discard values 40-48, since they unfairly favor 0-8 when we later do %10

```
       0    1    2    3    4    5    6
    ----------------------------------
0  |   0    1    2    3    4    5    6
1  |   7    8    9   10   11   12   13
2  |  14   15   16   17   18   19   20
3  |  21   22   23   24   25   26   27
4  |  28   29   30   31   32   33   34
5  |  35   36   37   38   39   __   __
6  |  __   __   __   __   __   __   __
```

`num % 10` will then give us:

```
       0    1    2    3    4    5    6
    ----------------------------------
0  |   0    1    2    3    4    5    6
1  |   7    8    9    0    1    2    3
2  |   4    5    6    7    8    9    0
3  |   1    2    3    4    5    6    7
4  |   8    9    0    1    2    3    4
5  |   5    6    7    8    9   __   __
6  |  __   __   __   __   __   __   __
```

So `num % 10 + 1` will change the 0-9 result to 1-10

```
       0    1    2    3    4    5    6
    ----------------------------------
0  |   1    2    3    4    5    6    7
1  |   8    9   10    1    2    3    4
2  |   5    6    7    8    9   10    1
3  |   2    3    4    5    6    7    8
4  |   9   10    1    2    3    4    5
5  |   6    7    8    9   10   __   __
6  |  __   __   __   __   __   __   __
```

### Solution

```java
class Solution extends SolBase {
    public int rand10() {
        while (true) {
            int num = 7 * (rand7() - 1) + (rand7() - 1);
            if (num < 40) {
                return num % 10 + 1;
            }
        }
    }
}
```

### Time/Space Complexity

- Time Complexity: `O(1)` average case, `O(∞)` worst case, since it's possible that `num` will consistently be larger than 40
- Space Complexity: `O(1)`

### Follow-up Solution

Reducing the number of calls to `rand7()` is not very beneficial, as the runtime will still be `O(1)` average case, `O(∞)` worst case

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/implement-rand10-using-rand7/discuss/312597)
- [github.com/RodneyShag](https://github.com/RodneyShag)
