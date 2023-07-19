---
id: 8frgm7vfmklgy8cvz3q3bgt
title: 285-inorder-successor-in-bst
desc: ''
updated: 1687263945381
created: 1687263660491
---
# 285. Inorder Successor in BST

## #dfs #medium #hard-for-me

Given the root of a binary search tree and a node p in it, return the in-order successor of that node in the BST. If the given node has no in-order successor in the tree, return null.

The successor of a node p is the node with the smallest key greater than p.val.

# 解题思路

首先用root val小于p找到第一个比p更大的node，然后再对左树dfs。一旦它有更小的符合条件的就会返回一个新的左node，但是如果没有就会往right走，最后会是null，recurse回来就是当前node。

```
Successor

public TreeNode successor(TreeNode root, TreeNode p) {
  if (root == null)
    return null;

  if (root.val <= p.val) {
    return successor(root.right, p);
  } else {
    TreeNode left = successor(root.left, p);
    return (left != null) ? left : root;
  }
}

Predecessor

public TreeNode predecessor(TreeNode root, TreeNode p) {
  if (root == null)
    return null;

  if (root.val >= p.val) {
    return predecessor(root.left, p);
  } else {
    TreeNode right = predecessor(root.right, p);
    return (right != null) ? right : root;
  }
}
```