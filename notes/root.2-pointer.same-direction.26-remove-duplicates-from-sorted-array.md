---
id: d9zyojfo74rik5fiqrq32hz
title: 26 Remove Duplicates from Sorted Arra
desc: ''
updated: 1688627650680
created: 1688627329511
---
## #2pointer #easy #iconic

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.

## 解题思路
思路是每次都要停在第一个unique的地方，在找到下一个不对的时候才要让slow+1;

```
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if (nums[i] != nums[j]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
}
```
