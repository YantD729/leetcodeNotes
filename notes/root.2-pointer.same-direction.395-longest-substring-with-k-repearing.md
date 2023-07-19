---
id: 7hbbs8kxk6h0482o58wljdk
title: 395 Longest Substring with K Repearing
desc: ''
updated: 1688642812332
created: 1688642501650
---
## #2pointer #medium #divideandconquer

Given a string s and an integer k, return the length of the longest substring of s such that the frequency of each character in this substring is greater than or equal to k.

## 解题思路

是对每一个substring进行判断，如果是true就返回长度；如果不是true就进一步切割。需要注意的是如果start不是i+1那么每一次迭代helper都从同一个起始，会造成stack overflow.

开始时如果k = 0或者1,返回的是string长度，因为都满足。

有一个不满足就接着运行分割部分，所以flag一开始是true，遍历过后还是true就return不进行下一个。

```
class Solution {
    public int longestSubstring(String s, int k) {
        if (s == null || s.length() == 0) return 0;
        if (k < 2) return s.length();
        return helper(s, 0, s.length(), k);
    }

    private int helper(String s, int l, int r, int k) {
        if (l >= r) return 0;

        int[] freq = new int[26];
        for (int i = l; i < r; i++) {
            freq[s.charAt(i) - 'a']++;
        }

        boolean flag = true;
        for (int i: freq) 
            if (i > 0 && i < k) flag = false;
        if (flag) return r - l;

        int start = 0;
        int best = 0;
        for (int i = l; i < r; i++) {
            if (freq[s.charAt(i) - 'a'] < k) {
                best = Math.max(best, helper(s, start, i, k));
                start = i + 1;
            }
        }
        best = Math.max(best, helper(s, start, r, k));
        return best;
    }
}
```