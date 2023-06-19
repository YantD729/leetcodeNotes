---
id: 3a5jynetol33bgpx2duoos6
title: '987'
desc: ''
updated: 1687144528196
created: 1687142842477
---
# 987. Vertical Order Traversal of a Binary Tree
## #dfs #hard #vertical-order<br>


Given the root of a binary tree, calculate the vertical order traversal of the binary tree.

For each node at position (row, col), its left and right children will be at positions (row + 1, col - 1) and (row + 1, col + 1) respectively. The root of the tree is at (0, 0).

The vertical order traversal of a binary tree is a list of top-to-bottom orderings for each column index starting from the leftmost column and ending on the rightmost column. There may be multiple nodes in the same row and same column. In such a case, sort these nodes by their values.

Return the vertical order traversal of the binary tree.
## 思路
这种垂直遍历的题目一般就是dfs/bfs的同时记录所需的列。<br>
Step 1 设置global variables 记录min column和max column <br>
Step 2 设置一个记录列的hashmap，并和当前行列一起traverse<br>
Step 3 以global variable 作为range进行一个for loop, 用lambda表达式进行排序，语言是：
`Collections.sort(list, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0])`这行代码是使用Java 8的lambda表达式进行排序的。这是一个自定义的比较器。

这段代码的意思是：对列表list中的元素进行排序，排序规则由lambda表达式`(a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]`定义。

这个lambda表达式的意思是，对于列表中的任意两个元素a和b：

如果a[0]（a的第一个元素）等于b[0]（b的第一个元素），那么比较a[1]和b[1]（它们的第二个元素）。a[1] - b[1]的结果决定了a和b的排序：如果结果是负数，那么a排在b之前；如果结果是正数，那么a排在b之后；如果结果是零，那么a和b的顺序不变。

如果a[0]不等于b[0]，那么比较a[0]和b[0]。a[0] - b[0]的结果决定了a和b的排序：如果结果是负数，那么a排在b之前；如果结果是正数，那么a排在b之后。<br>

`Collections.sort`对array, set, list都成立。<br>

之后，再将node.value从原本的数组中提取出来，按顺序加入新的Array并加入结果。<br>

Traverse 部份<br>

DFS Traverse的基本模板<br>

Step 1 先判定floor condition即node == null

（Step 1.5, 由于这题需要扩大范围，所以需要记录范围）

Step 2 然后处理本节点，把值和相应的row加入map。注意这里需要使用`map.putIfAbsent(currC, new ArrayList<int[]>());
    map.get(currC).add(new int[]{node.val, currR});`
Step 3 由于是DFS先traverse left后right

## 解法
 ```* Definition for a binary tree node.
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
    int minC = 0, maxC = 0;
    public List<List<Integer>> verticalTraversal(TreeNode root) {
        if (root == null) return null;
        Map<Integer, List<int[]>> map = new HashMap<>();
        traveresTree(map, 0, 0, root);

        List<List<Integer>> res = new ArrayList<>();

        for (int i = minC; i <= maxC; i++) {
            List<int[]> list = map.get(i);
            Collections.sort(list,(a,b) -> (a[1] == b[1]) ? a[0] - b[0] : a[1] - b[1]);
            List<Integer> ans = new ArrayList<>();
            for (int[] li: list) ans.add(li[0]);
            res.add(ans);
        }

        return res;
    }

    private void traveresTree(Map<Integer, List<int[]>> map, int currR, int currC, TreeNode node) {
        if (node == null) return;
        minC = Math.min(currC, minC);
        maxC = Math.max(currC, maxC);
        map.putIfAbsent(currC, new ArrayList<int[]>());
        map.get(currC).add(new int[]{node.val, currR});
        traveresTree(map, currR + 1, currC - 1, node.left);
        traveresTree(map, currR + 1, currC + 1, node.right);
    }
}
```