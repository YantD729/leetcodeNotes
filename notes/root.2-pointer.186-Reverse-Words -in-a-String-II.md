---
id: mttrnk4hp6petif1anjuvh6
title: 186-Reverse-Words -in-a-String-II
desc: ''
updated: 1688620602408
created: 1688611550991
---
## #2pointer #medium #reverseString

Given a character array s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by a single space.

Your code must solve the problem in-place, i.e. without allocating extra space.

## 解题思路

先把整体倒过来，再一个个倒过来，最后一个由于没有空格了要单独处理。

```
class Solution {
    public void reverseWords(char[] s) {
        reverse(s, 0, s.length - 1);
        int start = 0;
        for (int i = 1; i < s.length; i++) {
            char curr = s[i];
            if (curr == ' ') {
                reverse(s, start, i - 1);
                start = i+1;
            }
        }
        reverse(s, start, s.length - 1);
    }

    private void reverse(char[] s, int start, int end) {
        while (start < end) {
            char tmp = s[start];
            s[start] = s[end];
            s[end] = tmp;
            start++;
            end--;
        }
    }
}
```