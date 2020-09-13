### Solution

```java
class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> list = new ArrayList();

        for (int num = 1; num <= n; num++) {
            boolean divisibleBy3 = (num % 3 == 0);
            boolean divisibleBy5 = (num % 5 == 0);

            if (divisibleBy3 && divisibleBy5) {
                list.add("FizzBuzz");
            } else if (divisibleBy3) {
                list.add("Fizz");
            } else if (divisibleBy5) {
                list.add("Buzz");
            } else {
                list.add(String.valueOf(num));
            }
        }
        return list;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
