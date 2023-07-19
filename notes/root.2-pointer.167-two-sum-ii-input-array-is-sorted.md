---
id: svu0p4veou8ctjrgklhsx13
title: 167 Two Sum Ii Input Array Is Sorted
desc: ''
updated: 1688558998697
created: 1688558413010
---
## #2pointer #medium 

Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 < numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use only constant extra space.

## 解题思路

由于是sotred array, 其实自己找target的时候也知道是从两端开始找的，相当于一个最大一个最小，然后逐渐调节值。

需要注意的是，是1index，因此返回时需要+1.

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        if (nums.length < 2) return null;

        int left = 0;
        int right = nums.length - 1;

        while (left != right ) {
            if (nums[left] + nums[right] == target) {
                return new int[]{left+1, right+1};
            }
            if (nums[left] + nums[right] > target) {
                right--;
            }
            if (nums[left] + nums[right] < target) {
                left++;
            }
        }
        return null;        
    }
}
```