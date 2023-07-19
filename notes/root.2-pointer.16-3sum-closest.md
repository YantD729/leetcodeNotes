---
id: x4dt6jjjd6fcdxv9luis5l1
title: 16 3sum Closest
desc: ''
updated: 1688561528896
created: 1688561311184
---
## #2pointer #medium #iconic

Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.

## 解题思路

凡是sum想用2 pointer的都要先sort

这题就是在loop里call 2 pointer更新closest，等于target直接返回，不等于就比较更新closest，然后左右移动。

初始closest设置为nums[0]+nums[1]+nums[2]即可。

注意比较值大小要用到`Matn.abs(s)`

```
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        int closest_sum = nums[0] + nums[1] + nums[2];

        for (int i = 0; i < n - 2; i++) {
            int left = i + 1, right = n - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum == target) return sum;
                else if (sum < target) {left++;}
                else {right--;}
                if (Math.abs(sum - target) < Math.abs(closest_sum - target)) {closest_sum = sum;}
            }
        }

        return closest_sum;
    }
}
```