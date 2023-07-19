---
id: q6z39shxmm99hwytxzlm739
title: 1110-Delete-Nodes-And-Return-Forest
desc: ''
updated: 1688214371890
created: 1687154683542
---
# 1110. Delete Nodes And Return Forest

## #dfs #medium #bottom-up

## 解题思路

这题有所不同的是需要bottom up否则会错误地将要删除的node加进去

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
    HashSet<Integer> set = new HashSet<>();
    List<TreeNode> res = new ArrayList<>();
    public List<TreeNode> delNodes(TreeNode root, int[] to_delete) {
        if (root == null) return res;
        for (int i : to_delete) set.add(i);

        helper(root);

        if (!set.contains(root.val)) res.add(root);

        return res;
    }

    private TreeNode helper(TreeNode node) {
        if (node == null) return null;

        node.left = helper(node.left);
        node.right = helper(node.right);

        if (set.contains(node.val)) {
            if (node.left != null) res.add(node.left);
            if (node.right != null) res.add(node.right);
            return null;
        }

        return node;
    }
}
```