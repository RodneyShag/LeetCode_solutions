### Solution

```java
class Solution {
    public void reverseString(char[] s) {
        if (s == null) {
            return;
        }
        for (int i = 0; i < s.length / 2; i++) {
            swap(s, i, s.length - 1 - i);
        }
    }

    private void swap(char[] array, int i, int j) {
        char ch = array[i];
        array[i] = array[j];
        array[j] = ch;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
