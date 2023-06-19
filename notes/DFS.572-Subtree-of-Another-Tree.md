---
id: 608fhxjskf1iwucdug8tyxv
title: 572-Subtree-of-Another-Tree
desc: ''
updated: 1687154585823
created: 1687143416598
---
# 572-Subtree-of-Another-Tree

Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

这种题在比较tree是否一样/找subtree中很常见，一般是如果本node 正确了traverse其他的children，而在traverse中一旦当前node不符合就立刻停止。DFS在分治/自上而下中很常见。

Step 1 分辨本身是不是null,需要floor condition

Step 2 需要check本身是否符合条件，如果不符合

Step 3 进入左右子树的的判断，但是这个迭代是迭代函数自身

Traverse 部份
floor condition是二者都为null那就相等了，如果一个null一个不是null就不相等。

中间不是floor condition的时候一旦有一个节点不相等那就是不相等，如果相等就接着check下面是否相等（也是call自己）

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
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (root == null) return false;
        if (checkSame(root, subRoot)) return true;
        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
    }

    public boolean checkSame(TreeNode root, TreeNode sub) {
        if (root == null && sub == null) return true;
        if (root == null || sub == null) return false;
        if (root.val != sub.val) return false;
        return (checkSame(root.left, sub.left) && checkSame(root.right, sub.right));
    }
}
```