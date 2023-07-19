---
id: dsy4k16czrjgvqw769q4de0
title: 1658 Min Ops to Reduce X to Zero
desc: ''
updated: 1688914363574
created: 1688914218726
---
## #2pointer #medium #samedirection #iconic

You are given an integer array nums and an integer x. In one operation, you can either remove the leftmost or the rightmost element from the array nums and subtract its value from x. Note that this modifies the array for future operations.

Return the minimum number of operations to reduce x to exactly 0 if it is possible, otherwise, return -1.

## 解题思路

数组找最长就可以看一下滑动窗口了。

这题有一个就是，由于两端最小可以转化为中间最大，所以可以这么思考。

然后有个陷阱就是，找到最大值是在最后转化最小的。。。不然就会错

```
class Solution {
    public int minOperations(int[] nums, int x) {
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }

        int target = sum - x;
        int start = 0, end = 0, best = -1, curr = 0;
        while (end < nums.length) {
            curr += nums[end];
            while ( start <= end && curr > target) {
                curr -= nums[start];
                start++;
            }

            if (curr == target) {
                best = Math.max(best, end - start + 1);
            }

            end++;
        }

        return best == -1 ? -1 : nums.length - best;
    }
}
```