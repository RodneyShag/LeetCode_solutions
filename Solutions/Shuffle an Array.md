### Algorithm

- Loop through the array. For each element at index `i`, swap it with a random element in interval `[0, i]` inclusive.
- This swap ensures randomness in 2 ways:
  1. That each element in the array from `[0, i]` has an equal chance of being the ith element.
  1. That the original ith element has an equal chance of being anywhere in the array in `[0, i]`
- At each iteration of our `for` loop, the array from `[0, i]` has elements in random order.

### Solution

```java
class Solution {
    Random random = new Random();
    int[] original;
    int[] array;

    public Solution(int[] nums) {
         if (nums == null) {
            throw new IllegalArgumentException();
        }
        original = nums.clone();
        array = nums;
    }

    public int[] reset() {
        array = original.clone();
        return array;
    }

    public int[] shuffle() {
        for (int i = 1; i < array.length; i++) {
            int rand = random.nextInt(i + 1); // random int from [0, i+1) exclusive. Same as [0, i] inclusive
            swap(array, i, rand);
        }
        return array;
    }

    private void swap(int[] array, int i, int j) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n) to store our original array
