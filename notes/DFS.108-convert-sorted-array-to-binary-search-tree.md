---
id: n2l130f6mcbp033832gaj3y
title: 108-convert-sorted-array-to-binary-search-tree
desc: ''
updated: 1687256830872
created: 1687256272273
---
# 108. Convert Sorted Array to Binary Search Tree

## #dfs #easy #top-bottom

Given an integer array nums where the elements are sorted in ascending order, convert it to a 
height-balanced binary search tree.

##解题思路

和简单dfs的思路一样，因为可以将左右子树看成一个整块。

```
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null || nums.length == 0) return null;
        return helper(nums, 0, nums.length - 1);
    }

    private TreeNode helper(int[] nums, int l, int h) {
        if (l > h) return null;

        int mid = (l + h) / 2;
        TreeNode root = new TreeNode(nums[mid]);

        root.left = helper(nums, l, mid - 1);
        root.right = helper(nums, mid + 1, h);

        return root;
    }
}
```