---
id: 0ddlonch3pg6z0skkwv42bx
title: 212-word-search-II
desc: ''
updated: 1687764289760
created: 1687763191891
---
## #dfs #hard #backtrack

# 212. Word Search II

Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

## 解题思路

首先需要判断题目用trie解。

Intuitively, start from every cell and try to build a word in the dictionary. ```Backtracking (dfs)``` is the powerful way to exhaust every possible ways. Apparently, we need to do ```pruning``` when current character is not in any word.

How do we instantly know the current character is invalid? HashMap?

How do we instantly know what's the next valid character? LinkedList?

But the next character can be chosen from a list of characters. "Mutil-LinkedList"?

```=> Trie```
因此，这题分为三部分：
1）在solution中对棋盘每一个字母进行遍历。由于已经路过的会被标记，所以不用另找一个set来记录。

2）build trie。需要用一点ood的思想，对于每一个trienode，如果有对应的字母，则新建一个字母的array；每个词的字母全部添加完毕后再加入词本身。

3）然后对每一个字母进行dfs。首先判断p.next[c - 'a']是否为空，或者c本身是否为```'#'```即是否已经在本路线遍历过，再对他进行新的array。如果说p.word不是空则加入结果并将word变为null去重。

```
class Solution {
    class TrieNode {
        TrieNode[] next = new TrieNode[26];
        String word;
    }
    public List<String> findWords(char[][] board, String[] words) {
        List<String> res = new ArrayList<>();
        TrieNode root = buildTrie(words);
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                dfs(board, i, j, res, root);
            }
        }
        return res;
    }

    public void dfs (char[][] board, int i, int j, List<String> res, TrieNode p) {
        char c = board[i][j];
        if (c == '#' || p.next[c - 'a'] == null) return;
        p = p.next[c - 'a'];
        if (p.word != null) {
            res.add(p.word);
            p.word = null;
        }

        board[i][j] = '#';
        if (i > 0) dfs(board, i - 1, j, res, p);
        if (j > 0) dfs(board, i, j - 1, res, p);
        if (i < board.length - 1) dfs(board, i + 1, j, res, p);
        if (j < board[0].length - 1) dfs(board, i, j + 1, res, p);
        board[i][j] = c;
    }

    public TrieNode buildTrie(String[] words) {
        TrieNode root = new TrieNode();
        for (String w: words) {
            TrieNode p = root;
            for (char c: w.toCharArray()) {
                int i = c - 'a';
                if (p.next[i] == null) p.next[i] = new TrieNode();
                p = p.next[i];
            }
            p.word = w;
        }
        return root;
    }
}
```
