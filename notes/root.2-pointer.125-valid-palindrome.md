---
id: kzef1egy6t2eer2t2zqy9zq
title: 125 Valid Palindrome
desc: ''
updated: 1688523922824
created: 1688523186640
---
## #2pointer #easy #iconic

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

##解题思路

就没什么好说的，第一步变成chararray，然后从两头开始跑。

这道题注意的是需要character.isLetterOrDigit()函数

```
class Solution {
    public boolean isPalindrome(String s) {
        char[] c = s.toCharArray();
        for (int i=0, j = c.length-1; i<j;){
            if (!Character.isLetterOrDigit(c[i])) i++;
            else if (!Character.isLetterOrDigit(c[j])) j--;
            else if (Character.toLowerCase(c[i++])!=Character.toLowerCase(c[j--])) return false;
        }
        return true;
    }
}
```