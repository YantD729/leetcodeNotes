---
id: wlhn7a7x2nggk44ke2fvx7s
title: 694-number-of-distinct-islands
desc: ''
updated: 1688131378469
created: 1688131096848
---
## #dfs #medium #iconic

## 解题思路
这题其实是将岛屿当作路径来做，对于左右上下/路径端头进行标记，由于dfs的特性，如果到了端头会返回，然后加一个e，然后后面的端接着探索。

在Java中，List的添加和查询操作比StringBuilder的操作要慢。而且，由于我们是将List<Integer>添加到HashSet中，所以当比较两个列表是否相等时，需要逐一比较列表中的每个元素，这也会增加时间复杂度。

因此用StringBuilder来记录path会比用int array更好。

并且，mark本身的grid就行，然后对四周进行dfs。

这道题还是挺典型的dfs记录路径。

```
class Solution {
    private int[][] dir = {{0, -1}, {0, 1}, {-1, 0}, {1, 0}};
    public int numDistinctIslands(int[][] grid) {
        int n = grid.length, m = grid[0].length;
        Set<String> set = new HashSet();

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (grid[i][j] == 1) { 
                    StringBuilder path = new StringBuilder();
                    dfs(grid, i, j, path, "s"); // Start of dfs
                    set.add(path.toString());
                }
            }
        }

        return set.size();
    }

    private void dfs(int[][] grid, int x, int y, StringBuilder path, String dir) {
        if (x < 0 || y < 0 || x >= grid.length || y >= grid[0].length) return; 
        if (grid[x][y] == 0) return;

        path.append(dir);
        grid[x][y] = 0; // Mark node visited

        dfs(grid, x-1, y, path, "u");
        dfs(grid, x, y-1, path, "l");
        dfs(grid, x, y+1, path, "r");
        dfs(grid, x+1, y, path, "d");

        // End of current node, this is required,
        // otherwise two different shapes can be considered same, which is wrong
        path.append("e");  
    }
}
```