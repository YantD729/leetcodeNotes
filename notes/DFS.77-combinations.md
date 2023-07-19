---
id: d1x6n8kbl9d6st8djup7yq4
title: 77-combinations
desc: ''
updated: 1688219269647
created: 1688217973231
---
## #dfs #medium #iconic #pruning

## 解题思路

很普通的dfs题目

```
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> combine(int n, int k) {
        
        List<Integer> path = new ArrayList<>();
        //注意这里是直接dfs而不是一个forloop，可以理解为这是一个启动项，然后后面相当于连锁反应。start本身也包括在dfs的for loop里所以不用担心
        dfs(path, 0, 1, k, n);
        return res;
    }

    private void dfs(List<Integer> path, int count, int start, int k, int n) {
        //记住floor condition一定要加一个new array不然结果都是空的，还有一定要return！！
        if (count == k){ 
            res.add(new ArrayList(path)); 
            return;}
    
        if (start > n) return;

        for (int i = start; i <= n; i++) {
            path.add(i);
            //加了i，所以是从下一个开始loop。
            dfs(path, count + 1, i + 1, k, n);
            path.remove(path.size() - 1);
        }
    }
}
```

## 剪枝有技巧

就思考一下start最后不能超过你剩余需要找的数就行了。

```
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> prev = new ArrayList<>();
    public List<List<Integer>> combine(int n, int k) {
      dfs(n, k, 1);
      return res;
    }

    private void dfs(int n, int k, int start) {
      if (k == 0) {
        res.add(new ArrayList<>(prev));
        return;
      }
      for (int i = start; i <= n - (k - 1); i++) {
        prev.add(i);
        dfs(n, k - 1, i + 1);
        prev.remove(prev.size() - 1);
      }
    }
}
```