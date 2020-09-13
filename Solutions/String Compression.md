### Solution

```java
class Solution {
    public int compress(char[] array) {
        if (array == null || array.length == 0) {
            return 0;
        }
        int i = 0; // for reading
        int j = 0; // for writing

        while (i < array.length) {
            char currentChar = array[i];
            int count = 0;
            while (i < array.length && array[i] == currentChar) {
                count++;
                i++;
            }
            array[j++] = currentChar;
            if (count > 1) {
                for (char ch : String.valueOf(count).toCharArray()) {
                    array[j++] = ch;
                }
            }
        }
        return j;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(log n) due to our `toCharArray()` call which uses O(log<sub>10</sub> n) space, where the 10 represents the number of possible digits 0-9.

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
