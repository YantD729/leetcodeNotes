---
id: il5wzkn1tgsuf5a9ucj1esa
title: 1004 Max Consecutive Ones Iii
desc: ''
updated: 1688911771147
created: 1688906489382
---
## #2pointer #medium #samedirection #iconic

Given a binary array nums and an integer k, return the maximum number of consecutive 1's in the array if you can flip at most k 0's.

## 解题思路

同向指针都是相对速度的问题。如果zeros > k了那就
相对速度不变往前挪一个位置，说明要减一个0，不管这个0在哪。但他永远也不会比之前的最大值小，因为没有管这个0在哪。
```
class Solution {
    public int longestOnes(int[] nums, int k) {
        if (nums == null || nums.length == 0) return 0;

        int start = 0, end = 0, zeros = 0;
        while (end < nums.length) {
            if (nums[end] == 0) zeros++;
            end++;
            if (zeros > k) {
                if (nums[start] == 0) zeros--;
                start++;
            }
        }
        return end - start; 
    }
}
```
实在想不通您就用while + Math.max好了，缺点是每次都要更新一次。计数和k比较，不要用-- < 0这种奇怪的方式。
```
class Solution {
    public int longestOnes(int[] nums, int k) {
        if (nums == null) {
            throw new IllegalArgumentException("Input array is null");
        }

        int start = 0;
        int end = 0;
        int zeros = 0;
        int maxCount = 0;

        while (end < nums.length) {
            if (nums[end] == 0) {
                zeros++;
            }
            end++;
            while (zeros > k) {
                if (nums[start] == 0) {
                    zeros--;
                }
                start++;
            }
            maxCount = Math.max(maxCount, end - start);
        }

        return maxCount;
    }
}
```