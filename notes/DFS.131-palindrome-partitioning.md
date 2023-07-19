---
id: v0kzpm0m1kdi6e2ybjyjvxd
title: 131-palindrome-partitioning
desc: ''
updated: 1688215363150
created: 1688214331997
---
## #dfs #mediun #iconic

Given a string s, partition s such that every 
substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

# 解题思路

凡是这种多个解的都是dfs，要的就是挪走前一个解在判断。

这种题目都需要记录res和path，path是当前解，res是所有解的集合。

这道题还结合了就是判断palidrome，是start和end`双指针`判断

```
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        List<String> path = new ArrayList<>();
        helper(0, s, path, res);
        return res;
    }

    private void helper(int idx, String s, List<String> path,  List<List<String>> res) {
        if (idx == s.length()) {
            res.add(new ArrayList<String> (path));
            return;
        }

        for (int i = idx; i < s.length(); i++) {
            if (isPali(idx, i, s)) {
                path.add(s.substring(idx, i + 1));
                helper(i + 1, s, path, res);
                path.remove(path.size() - 1);
            }
        }

    }

    private boolean isPali(int start, int end, String str) {
        while (start < end) {
            if (str.charAt(start++) != str.charAt(end--)) return false;
        }
    return true;
    }
}
```