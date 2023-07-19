---
id: 5ptym4otm46qb88c5z6858q
title: 34-Find-First-and-Last-Position-of-Element-in-Sorted-Array
desc: ''
updated: 1687700338821
created: 1687697290199
---
# 34. Find First and Last Position of Element in Sorted Array

## #bst #medium

Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

# 解题思路

先找一个再找一个，因为两个找法不一样，第一个找lo就需要最后是lo + 1得到，反之亦然。

```
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] ans = new int[2];
        int lo = 0;
        int hi = nums.length - 1;
        int reslo = -1;
        int reshi = -1;

        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] >= target) hi = mid - 1;
            else lo = mid + 1;
        }
        if (lo < nums.length && lo >= 0 && nums[lo] == target) reslo = lo;

        lo = 0;
        hi = nums.length - 1;

        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] > target) hi = mid - 1;
            else lo = mid + 1;
        }
        if (hi < nums.length && hi >= 0 && nums[hi] == target) reshi = hi;

        ans[0] = reslo;
        ans[1] = reshi;

        return ans;
    }
}
```
