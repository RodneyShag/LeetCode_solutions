### Tricks

- Use arrays as data structure for the words.
- Split the number at each comma into groups of 3 digits. Create a function to convert 3-digit numbers to words.
- Don't forget to consider negative numbers, and 0.

### Solution

```java
class Solution {
    private String[] first20 = {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
    private String[] tens = {"", "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
    private String[] bigs = {"", "Thousand", "Million", "Billion"};

    public String numberToWords(int num) {
        if (num < 0) {
            return "Negative " + numberToWords(-1 * num);
        } else if (num == 0) {
            return "Zero";
        }

        int bigsIndex = 0;
        StringBuffer sb = new StringBuffer();

        // Create the string from right to left, inserting in the front.
        while (num > 0) {
            if (num % 1000 != 0) {
                sb.insert(0, numToWords100(num % 1000) + bigs[bigsIndex] + " ");
            }
            num /= 1000;
            bigsIndex++;
        }

        return sb.toString().trim();
    }

    private String numToWords100(int num) { // assumes 0 < num < 1000
        if (num == 0) {
            return "";
        } else if (num < 20) {
            return first20[num] + " ";
        } else if (num < 100) {
            return tens[num / 10] + " " + numToWords100(num % 10);
        } else {
            return first20[num / 100] + " Hundred " + numToWords100(num % 100);
        }
    }
}
```

### Time/Space Complexity

- Time Complexity: O(1)
- Space Complexity: O(1)
