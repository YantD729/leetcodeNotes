---
id: kuctjmvfxx33djaptlhu5wg
title: 1423-Maximum-points-obtained-from-cards
desc: ''
updated: 1689686845210
created: 1689686577213
---
## #medium #iconic

There are several cards arranged in a row, and each card has an associated number of points. The points are given in the integer array cardPoints.

In one step, you can take one card from the beginning or from the end of the row. You have to take exactly k cards.

Your score is the sum of the points of the cards you have taken.

Given the integer array cardPoints and the integer k, return the maximum score you can obtain.

## 解题思路

感觉前缀和和sliding window+dp很像，主要是要用array记录前缀和。

这题两端所以需要记录两遍前缀和。和dfs问题不同，前缀和比较简单，是一维，可预测的，所以叫记录结果。

快的做法是第二种，只记录开头那个，然后用sliding window思路解。_注意初始res = sum。_

class Solution {
    public int maxScore(int[] cardPoints, int k) {
        int n = cardPoints.length;

        int[] headSum = new int[k + 1];
        int[] rearSum = new int[k + 1];
        int res = 0;

        for (int i = 0; i < k; i++) {
            headSum[i + 1] = headSum[i] + cardPoints[i];
            rearSum[i + 1] = rearSum[i] + cardPoints[n - 1 - i];
        }

        for (int i = 0; i <= k ; i++) {
            int currSum = headSum[i] + rearSum[k - i];
            res = Math.max(currSum, res);
        }

        return res;
     }
}

class Solution {
    public int maxScore(int[] cardPoints, int k) {
        int n = cardPoints.length;

        int sum = 0, res = 0;

        for (int i = 0; i < k; i++) {
            sum += cardPoints[i];
        }

        if (k >= n) return sum;

       res = sum;

        for (int i = k - 1; i >= 0 ; i--) {
            sum -= cardPoints[i];
            sum += cardPoints[n - k + i];
            res = Math.max(sum, res);
        }

        return res;
     }
}
