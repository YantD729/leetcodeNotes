---
id: 1xj3b8yvm735e1skx40782p
title: 647 Palindromic Substrings
desc: ''
updated: 1688558307708
created: 1688558227057
---
## #2pointer #medium #iconic

Given a string s, return the number of palindromic substrings in it.

A string is a palindrome when it reads the same backward as forward.

A substring is a contiguous sequence of characters within the string.

## 解题思路

就很简单！！brute force count一下即可。

```
class Solution {
    public int countSubstrings(String s) {
        int count = 0;
        for (int i = 0; i < s.length(); i++) {
            count += palidromeNum(s, i, i);
            count += palidromeNum(s, i, i+1);
        }
        return count;
    }

    private int palidromeNum(String s, int i, int j) {
        int count = 0;
        while (i >= 0 && j < s.length() && s.charAt(i) == s.charAt(j)) {
            i--;
            j++;
            count++;
        }
        return count;
    }
}
```