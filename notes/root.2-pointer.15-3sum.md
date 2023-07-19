---
id: bfno31goff3mnwto6l2lfzs
title: 15 3sum
desc: ''
updated: 1688560852720
created: 1688560309910
---
## #2pointer #medium #iconic

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

## 解题思路

其实就是对于每个i，call一遍two sum。

首先对于nums[i]需要有判断，由于和是0，所以如果当前值比0大就不用考虑，如果相同就跳过（因为要求不能有重复的）算是一种剪枝。

然后对于call的two sum，为0的时候需要用到Arrays.asList().需要注意的是由于还可以继续找解，所以也是要先跳过相同的，这时候不能直接return，要接着2 pointer滑动，最后再return array。

Time Complexity: `O(n2)`. twoSumII is O(n), and we call it n times.

Sorting the array takes `O(nlog⁡n)`, so overall complexity is `O(nlog⁡n+n2)`. This is asymptotically equivalent to O(n2)

Space Complexity: from`O(log⁡n) to O(n)`, depending on the implementation of the sorting algorithm. For the purpose of complexity analysis, we ignore the memory required for the output.

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) {
                return res;
            }

            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }

            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum > 0) right --;
                else if (sum < 0) left ++;
                else {
                    res.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while (right > left && nums[right] == nums[right - 1]) right--;
                    while (right > left && nums[left] == nums[left + 1]) left++;

                    right--;
                    left++;
                    
                }

            }
        }
        return res;
    }
}

```