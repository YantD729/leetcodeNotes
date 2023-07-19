---
id: qt69za57h8w1wqn6zq31dld
title: 669-Trim-a-Binary-Search-Tree
desc: ''
updated: 1687184525527
created: 1687184388967
---
# 669. Trim a Binary Search Tree
## #dfs #medium #bottom-top
Given the root of a binary search tree and the lowest and highest boundaries as low and high, trim the tree so that all its elements lies in [low, high]. Trimming the tree should not change the relative structure of the elements that will remain in the tree (i.e., any node's descendant should remain a descendant). It can be proven that there is a unique answer.

Return the root of the trimmed binary search tree. Note that the root may change depending on the given bounds.

## 解题思路

这题就真的很绝，是从下而上但不完全，中间需要跳步的处理，具体就是跳过这个节点，处理下一个符合的节点，这样可以和后面连接。

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode trimBST(TreeNode root, int l, int h) {
        if (root == null) return root;

        if (root.val < l) return trimBST(root.right, l, h);
        if (root.val > h) return trimBST(root.left, l, h);

        root.left = trimBST(root.left, l, h);
        root.right = trimBST(root.right, l, h);

        return root;
    }
}

```

