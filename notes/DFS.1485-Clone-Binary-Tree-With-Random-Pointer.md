---
id: recf6ijjhff3ebsiv9t4zld
title: 1485-Clone-Binary-Tree-With-Random-Pointer
desc: ''
updated: 1687182702797
created: 1687181666725
---
# 1485. Clone Binary Tree With Random Pointer

## #dfs #medium #top-bottom

## 解题思路

这题一开始我以为很难，后来发现那个random和普通的处理起来没有区别，只不过也是自上而下。这种需要构建的很多都是自上而下。

同时，由于随机节点是随机的，如果不用hashmap记录会让随机节点的指针到处乱窜，所以需要额外的hashmap。

```
/**
 * Definition for Node.
 * public class Node {
 *     int val;
 *     Node left;
 *     Node right;
 *     Node random;
 *     Node() {}
 *     Node(int val) { this.val = val; }
 *     Node(int val, Node left, Node right, Node random) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *         this.random = random;
 *     }
 * }
 */

class Solution {
    public NodeCopy copyRandomBinaryTree(Node root) {
        Map<Node, NodeCopy> map = new HashMap<>();
        return dfs(root, map);
    }

    private NodeCopy dfs(Node curr, Map<Node, NodeCopy> map) {
        if (curr == null) return null;

        if (map.containsKey(curr)) return map.get(curr);

        NodeCopy cp = new NodeCopy(curr.val);
        map.put(curr, cp);

        cp.left = dfs(curr.left, map);
        cp.right = dfs(curr.right, map);
        cp.random = dfs(curr.random, map);

        return cp;
    }
}
```