### Algorithm

We keep track of the mod values in buckets for each number we read. We can do this
by creating `k` buckets where bucket `i` counts each number `n` where `n % k = i`.

Notice that each bucket has a corresponding "complement" bucket. That is, if we take
the mod value of one bucket and add it to the mod value of another bucket, we get `k`.

```
Bucket   Complement Bucket
------   -----------------
  0            0
  1           k-1
  2           k-2
  3           k-3
       ...
 k-3           3
 k-2           2
 k-1           1
```

As we come across each number, we find its corresponding complement bucket. Each number in
this complement bucket can be paired with our original number to create a sum divisible by `k`.

### Solution

```java
class Solution {
    public int numPairsDivisibleBy60(int[] time) {
        int [] bucket = new int[60];
        int count = 0;
        for (int t : time) {
            int modValue = t % 60;
            count += bucket[(60 - modValue) % 60]; // adds # of elements in complement bucket.
            bucket[modValue]++;                    // saves in bucket.
        }
        return count;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n + k)
- Space Complexity: O(k)

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/discuss/304465)
- [github.com/RodneyShag](https://github.com/RodneyShag)
