### Provided Code

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
}
```

### Solution

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        } else if (p == null || q == null) {
            return false;
        }
        return p.val == q.val
            && isSameTree(p.left, q.left)
            && isSameTree(p.right, q.right);
    }
}
```

### Time/Space Complexity

Let `m` be number of `TreeNodes` in `p`. Let `n` be number of `TreeNodes` in `q`.

-  Time Complexity: O(min(m + n))
- Space Complexity: O(min(m + n))

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/same-tree/discuss/457479)
- [github.com/RodneyShag](https://github.com/RodneyShag)
