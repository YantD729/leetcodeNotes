---
id: 7wer3xlvsnczjvk9lph6zl3
title: 264-ugly-number-ii
desc: ''
updated: 1689556575514
created: 1689556332488
---
## #medium #map ? #dp

An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.

Given an integer n, return the nth ugly number.

## 解题思路

我咋觉得这题更像个dp啊。。和map扯上边的唯一可能就是说用index找之前的数字然后乘

我觉得这题其实重点是理解ugly number的规律。

class Solution {
    public int nthUglyNumber(int n) {
        int[] ugly = new int[n];
        ugly[0] = 1;
        int idx2 = 0, idx3 = 0, idx5 = 0;
        int factor2 = 2, factor3 = 3, factor5 = 5;
        for (int i = 1; i < n; i++) {
            int min = Math.min(Math.min(factor2, factor3), factor5);
            ugly[i] = min;
            if (factor2 == min) factor2 = 2*ugly[++idx2];
            if (factor3 == min) factor3 = 3*ugly[++idx3];
            if (factor5 == min) factor5 = 5*ugly[++idx5];
        }
        return ugly[n - 1];
    }
}
