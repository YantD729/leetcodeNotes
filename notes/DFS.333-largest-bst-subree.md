---
id: oczboeun1aye44au8fi213b
title: 333-largest-bst-subree
desc: ''
updated: 1687260362909
created: 1687260230869
---
# 333. Largest BST Subtree

## #dfs #medium #top-bottom

Given the root of a binary tree, find the largest 
subtree
, which is also a Binary Search Tree (BST), where the largest means subtree has the largest number of nodes.

A Binary Search Tree (BST) is a tree in which all the nodes follow the below-mentioned properties:

The left subtree values are less than the value of their parent (root) node's value.
The right subtree values are greater than the value of their parent (root) node's value.
Note: A subtree must include all of its descendants.

## 解题思路

其实这题主要在于需要判断是否是bst。 如果已经是bst了，只需要用size就好了。注意size是左右相加的值而不是仅仅一条线。

```
class Solution {
    public int largestBSTSubtree(TreeNode root) {
        if (root == null) return 0;

        if (isBST(root, Integer.MAX_VALUE, Integer.MIN_VALUE)) return size(root);

        return Math.max(largestBSTSubtree(root.left), largestBSTSubtree(root.right));
    }

    private boolean isBST(TreeNode curr, int max, int min) {
        if (curr == null) return true;

        if (curr.val >= max || curr.val <= min) return false;

        return (isBST(curr.left, curr.val, min) && isBST(curr.right, max, curr.val));
    }

    private int size(TreeNode node) {
        if (node == null) return 0;

        return size(node.left) + size(node.right) + 1;
    }
}
```