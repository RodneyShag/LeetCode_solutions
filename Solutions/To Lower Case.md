### Algorithm

This problem forbids us from using `str.toLowerCase()` which is a simple working solution. We will code a similar function below

- We assume only English letters (A to Z) need to be lowercased
- Uppercase letters are numbers 65 to 90 in an [ASCII table](http://www.asciitable.com)
- Lowercase letters are numbers 97 to 122 in the same table
- Notice uppercase letters and lowercase letters differ by 32 in the ASCII table:
    - 'A' + 32 = 65 + 32 = 97 = 'a'    
    - 'Z' + 32 = 97 + 32 = 122 = 'z'

### Solution

```java
class Solution {
    public String toLowerCase(String s) {
        if (s == null) {
            return s;
        }
        char[] arr = s.toCharArray();
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] >= 'A' && arr[i] <= 'Z') {
                arr[i] += 32;
            }
        }
        return new String(arr);
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(s)
- Space Complexity: O(s)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
