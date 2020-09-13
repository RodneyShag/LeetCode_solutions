### Assumptions

- Provided array is not null
- Provided array is not empty
- Majority element always exists in provided array

### Algorithm

- Loop through the array. At each index `i`, we treat the array as 2 pieces
    - prefix as `[0, i)`
    - suffix as `[i, end]`
- Main idea: If we don't have the majority element in the prefix, then the suffix must have a majority element, and this majority element will also be the majority element for the entire array.

### Solution

```java
class Solution {
    public int majorityElement(int[] array) {
        int count = 0;
        Integer candidate = null;

        for (int num : array) {
            if (count == 0) { // no majority element in prefix
                candidate = num; // selects new candidate majority element
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Additional Notes

In the case that the majority element does not necessarily exist in the provided array, we would take the output of `majorityElement()` and test to see if our candidate qualifies as the majority element (by checking that the number makes up at least half of the array):

```java
boolean isCandidateValid(int[] array, int candidate) {
    long count = Arrays.stream(array).filter(a -> (a == candidate)).count();
    return count * 2 > array.length;
}
```

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
