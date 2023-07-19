---
id: 9tb5b6dvtwaq7j2jbhf6yqa
title: 11 Container with Most Wate
desc: ''
updated: 1688621117254
created: 1688621002234
---
## #2pointer #medium #iconic

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

## 解题思路

就是左右找，但是如果有一方比一方高，需要先挪动矮的一方比较，这样才有可能找到最大值，如果都相等了就往中间挪动试试

```
class Solution {
    public int maxArea(int[] height) {
        int l = 0;
        int r = height.length - 1;
        int max = (r - l) * Math.min(height[r], height[l]);
        while (l < r) {
            if (height[l] < height[r]) l += 1;
            else if (height[l] > height[r]) r -= 1;
            else {
                l += 1;
                r -= 1;
            }
            max = Math.max(max, (r - l) * Math.min(height[r], height[l]));
        }

        return max; 
    }
}
```