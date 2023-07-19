---
id: s1ngjc1x7862s4ca3whyiox
title: 680 Valid Palindrome
desc: ''
updated: 1688525683516
created: 1688525518394
---
## #2pointer #easy #iconic

Given a string s, return true if the s can be palindrome after deleting at most one character from it.

## 解题思路

这道题主要要抓住palindrome的重点，即回文数左右减的时候，内部的sub palindrome也是回文数。因此其实这道题要求的是“跳过一个index”来找解法。由于只能跳过一次，所以只是主函数里面有一次判断/更改即可。

```
class Solution {
    public boolean validPalindrome(String s) {
        int i = 0;
        int j = s.length() - 1;
         while(i < j) {
            if (s.charAt(i) != (s.charAt(j))) 
                return (isPalindrom(s, i+1, j) || isPalindrom(s, i, j - 1));
            i++;
            j--;
        }
        return true;
        
    }

    private boolean isPalindrom(String s, int i, int j) {
        while(i < j) {
            if (s.charAt(i) != (s.charAt(j))) return false;
            i++;
            j--;
        }
        return true;
    }
}
```