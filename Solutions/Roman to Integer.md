### Assumption

We assume input is a valid Roman numeral. For example, we assume we will not get `IM` as a Roman numeral (since `I` cannot be placed immediately before `M`)

### Algorithm

1. Create a `Map<Character, Integer>` that maps Roman Numeral Characters to their values.
1. Initialize a running `sum` to 0.
1. Loop through all characters of the array except for the last character.
    - if current character's value is less than next character's value, subtract current character's value from `sum`
    - else, add current character's value to `sum`.
1. For the last character, add it's value to the running `sum`, and return `sum`.


### Solution

```java
class Solution {
    public int romanToInt(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        Map<Character, Integer> map = new HashMap();
        map.put('I', 1);
        map.put('V', 5);
        map.put('X', 10);
        map.put('L', 50);
        map.put('C', 100);
        map.put('D', 500);
        map.put('M', 1000);

        int sum = 0;
        for (int i = 0; i < s.length() - 1; i++) {
            if (map.get(s.charAt(i)) < map.get(s.charAt(i + 1))) {
                sum -= map.get(s.charAt(i));
            } else {
                sum += map.get(s.charAt(i));
            }
        }
        return sum + map.get(s.charAt(s.length() - 1));
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
