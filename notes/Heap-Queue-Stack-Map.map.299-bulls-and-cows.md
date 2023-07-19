---
id: nqlwdltabkonu7dkfgwsxdy
title: 299-bulls-and-cows
desc: ''
updated: 1689303033332
created: 1689302906745
---
## #medium #map #iconic

You are playing the Bulls and Cows game with your friend.

You write down a secret number and ask your friend to guess what the number is. When your friend makes a guess, you provide a hint with the following info:

The number of "bulls", which are digits in the guess that are in the correct position.
The number of "cows", which are digits in the guess that are in your secret number but are located in the wrong position. Specifically, the non-bull digits in the guess that could be rearranged such that they become bulls.
Given the secret number secret and your friend's guess guess, return the hint for your friend's guess.

The hint should be formatted as "xAyB", where x is the number of bulls and y is the number of cows. Note that both secret and guess may contain duplicate digits.

## 解题思路

好像因为是数字用int[]来记录freq挺常见的，其实是模拟hashset。同样的还有char[26].难点在于用>0, <0来计算是否是同一位置。

class Solution {
    public String getHint(String secret, String guess) {
        int[] cnts = new int[10];
        int cows = 0, bulls = 0;
        int n = secret.length();
        for (int i = 0; i < n; i++) {
            char s = secret.charAt(i);
            char g = guess.charAt(i);
            if (s == g) bulls++;
            else {
                if (cnts[s - '0'] < 0) cows++;
                if (cnts[g - '0'] > 0) cows++;
                    cnts[s - '0']++;
                    cnts[g - '0']--;
            }
        }
        StringBuilder sb = new StringBuilder();
        sb.append(bulls);
        sb.append('A');
        sb.append(cows);
        sb.append('B');
        return sb.toString();
    }
}