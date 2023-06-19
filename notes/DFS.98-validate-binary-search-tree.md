---
id: t9x3egtb2h8kf4mha5tg9xt
title: 98-validate-binary-search-tree
desc: ''
updated: 1687156193791
created: 1687156077695
---
# 98. Validate Binary Search Tree

## #dfs #medium #top-bottom

## 解题思路

就是和一般的找对称一样，先看本身，然后在看后面的是否符合bst的特点

```
public class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }
    
    public boolean isValidBST(TreeNode root, long minVal, long maxVal) {
        if (root == null) return true;
        if (root.val >= maxVal || root.val <= minVal) return false;
        return isValidBST(root.left, minVal, root.val) && isValidBST(root.right, root.val, maxVal);
    }
}
```