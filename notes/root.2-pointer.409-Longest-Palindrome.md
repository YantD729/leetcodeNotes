---
id: kn96fznzaxupasjfqs3696b
title: 409-Longest-Palindrome
desc: ''
updated: 1688522552215
created: 1688521655816
---
## #2pointer #easy

Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.

Letters are case sensitive, for example, "Aa" is not considered a palindrome here.

## 解题思路

128个boolean然后翻来翻去，有点像bitwise里那种～思路

注意的是for loop中只对string里有的character进行先翻转和判断，因此才能说boolean是false时加2.最后小于length加一的是放在中间的字母。

```
class Solution {
    public int longestPalindrome(String s) {
        boolean[] map = new boolean[128];
        int res = 0;
        for (char c: s.toCharArray()) {
            map[c] = !map[c];
            if (!map[c]) res += 2;
        }
        if (res < s.length()) res++;
        return res;
    }
}
```