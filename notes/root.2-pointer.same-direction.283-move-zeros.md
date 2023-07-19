---
id: g78eysolyzgnpqj83xdo3ay
title: 283 Move Zeros
desc: ''
updated: 1688624947143
created: 1688622788680
---
## #2pointer #easy

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

## 解题思路

移动零的这道题，主要是如果不是零就一起行动，保持一个相对静止，如果有零就会有速度差，fast在这个零状态下会再空一个接着换回去。

第一个while条件是fast比array length小，第二个就是从slow开始换0。无论如何fast都加，但是slow只有不是0时加，故fast在if括号外。

如果是brute force的方法就是，Move all the 0's to the end of array.

All the non-zero elements must retain their original order.这两个需求不矛盾，可以先遍历记数0，再遍历加入不是0的，然后加0.

双指针解法如下：

```
class Solution {
    public void moveZeroes(int[] nums) {
        int fast, slow;
        fast = slow = 0;
        while (fast < nums.length) {
            if (nums[fast] != 0) {
                nums[slow] = nums[fast];
                slow++;
            }
            fast++;
        }
        for (int i = slow; i < nums.length; i++) {
            nums[i] = 0;
        }
        return;
    }
}

```