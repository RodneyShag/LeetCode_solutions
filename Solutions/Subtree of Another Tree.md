### Algorithm

Use [Preorder traversal](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Binary%20Tree%20Preorder%20Traversal.md) to convert each tree into a String.

Replace each `null` with an `X`. This is necessary to distinguish between trees such as

```
  1         1
 /    vs.    \
2             2
```

```
  1
 /     would incorrectly be "12". Now it's "12X"
2
```

```
  1
   \   would incorrectly be "12". Now it's "1X2"
    2
```

Since each `TreeNode` value is an `int`, we can safely append a `#` symbol in front of it to distinguish between the following trees:

```
  1            12
 /     vs.     /
23            3
```

```
  1
 /   would incorrectly be "123X". Now it's "#1#23X"
23
```

```
  1
 /   would incorrectly be "123X". Now it's "#1#23X"
23
```


After converting the 2 trees to 2 Strings, iff String 2 is a substring of String 1, then tree 2 is a subtree of tree 1.

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
    public boolean isSubtree(TreeNode t1, TreeNode t2) {
        StringBuffer sb1 = new StringBuffer();
        StringBuffer sb2 = new StringBuffer();
        getPreorder(t1, sb1);
        getPreorder(t2, sb2);
        return sb1.indexOf(sb2.toString()) != -1;
    }

    private void getPreorder(TreeNode node, StringBuffer sb) {
        if (node == null) {
            sb.append("X");
            return;
        }
        sb.append("#" + node.val);
        getPreorder(node.left, sb);
        getPreorder(node.right, sb);
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(m + n) if .indexOf() uses KMP algorithm.
- Space Complexity: O(m + n)

[Java's implementation for .indexOf() for Strings](http://hg.openjdk.java.net/jdk8/jdk8/jdk/file/tip/src/share/classes/java/lang/String.java#l1740) is naively O(n<sup>2</sup>) since it doesn't use the KMP algorithm! If `.indexOf()` is this slow for `StringBuffer`, then use this [O(n) implementation of KMP algorithm](https://github.com/RodneyShag/LeetCode_solutions/blob/master/Solutions/Implement%20strStr.md) instead.

### Links

- [Discuss on LeetCode](https://leetcode.com/problems/subtree-of-another-tree/discuss/361602)
- [github.com/RodneyShag](https://github.com/RodneyShag)
