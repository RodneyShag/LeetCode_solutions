### Provided Code

```java
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) {
      val = x;
    }
}
```

### Solution

```java
class Solution {
    public TreeNode sortedArrayToBST(int[] sortedArray) {
        if (sortedArray == null) {
            return null;
        }
        return createBST(sortedArray, 0, sortedArray.length - 1);
    }

    private TreeNode createBST(int[] sortedArray, int startIndex, int endIndex) {
        if (startIndex > endIndex) {
            return null;
        }
        int mid = (startIndex + endIndex) / 2;
        TreeNode root = new TreeNode(sortedArray[mid]);
        root.left  = createBST(sortedArray, startIndex, mid - 1);
        root.right = createBST(sortedArray, mid + 1, endIndex);
        return root;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n) since we're creating a Binary Search Tree
