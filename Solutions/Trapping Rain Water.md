# Solution 1

### Algorithm

For each index, 2 walls (the tallest wall anywhere to the left, and to the right) together determine the amount of water the index will hold. We can calculate this iteratively.

### Code

```java
class Solution {
    public int trap(int[] height) {
        if (height == null || height.length <= 1) {
            return 0;
        }
        int size = height.length;

        // Calculate left maxes
        int[] leftMax = new int[size];
        leftMax[0] = height[0];
        for (int i = 1; i < size; i++) {
            leftMax[i] = Math.max(leftMax[i - 1], height[i]);
        }

        // Calculate right maxes
        int[] rightMax = new int[size];
        rightMax[size - 1] = height[size - 1];
        for (int i = size - 2; i >= 0; i--) {
            rightMax[i] = Math.max(rightMax[i + 1], height[i]);
        }

        // Calculate amount of water that can be stored above each spot on histogram
        int water = 0;
        for (int i = 1; i < size - 1; i++) {
            water += Math.min(leftMax[i], rightMax[i]) - height[i];
        }
        return water;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)


# Solution 2

From [LeetCode Official Solutions - Approach 4](https://leetcode.com/problems/trapping-rain-water/solution/) - this solution aims to optimize our space complexity

### Algorithm

- At `i`, as long as rightMax > leftMax, the water trapped depends on leftMax.
    - In this case, if at the current `i` we have a new leftMax, we simply update leftMax, otherwise, we add the trapped water at that location.
- A symmetric argument can be made for when rightMax < leftMax.
- We will use 2 pointers, 1 on each end of the array, coming inwards to calculate the solution. Traversing it this way lets us best utilize the tallest wall we've seen thus far.

### Code

```java
class Solution {   
    public int trap(int[] height) {
        if (height == null || height.length <= 1) {
            return 0;
        }

        int left = 0;
        int right = height.length - 1;
        int maxLeft = 0;
        int maxRight = 0;
        int water = 0;

        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] >= maxLeft) {
                    maxLeft = height[left];
                } else {
                    water += maxLeft - height[left];
                }
                ++left;
            } else {
                if (height[right] >= maxRight) {
                    maxRight = height[right];
                } else {
                    water += maxRight - height[right];
                }
                --right;
            }
        }
        return water;
    }
}

```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)


# Links

- [github.com/RodneyShag](https://github.com/RodneyShag)
