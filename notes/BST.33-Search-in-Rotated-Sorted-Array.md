---
id: ofy73jeei8xlbpv7a407w2n
title: 33-Search-in-Rotated-Sorted-Array
desc: ''
updated: 1687749734032
created: 1687745513693
---
# 33. Search in Rotated Sorted Array

## #medium #bst

## 解题思路
这个解题需要注意的是即便旋转了，它也是单调递增的，不存在首尾会覆盖的情况。并且由于hi就算有序也会比mid大，所以一开始需要比较lo和mid才能看出是否有序。

因此，pseudo code应该大概是这样：

if (nums[lo] < nums[mid]) 说明前半段是有序数组，在这个前提下：

if (target在nums[lo, mid]的区间内) hi就等于mid - 1
如果不在那就lo = mid + 1（去另一半找）

else同理，看target在不在[mid, hi]这个区间，在lo = mid + 1, 不在hi = mid - 1.

最后没有就return -1.

基本思路是寻找单调区间。

_由于是递增的array，如果不是有序区间，起始只可能比结束大。因此只要断定起始比结束小，就是有序区间。_

_用小于等于是说不严格单调递增也算在lo-mid里。_

**最后返回的要判断lo是否等于target！**

```
public class Solution {
    public int search(int[] A, int target) {
        int lo = 0;
        int hi = A.length - 1;
        while (lo < hi) {
            int mid = (lo + hi) / 2;
            if (A[mid] == target) return mid;
            
            if (A[lo] <= A[mid]) {
                if (target >= A[lo] && target < A[mid]) {
                    hi = mid - 1;
                } else {
                    lo = mid + 1;
                }
            } else {
                if (target > A[mid] && target <= A[hi]) {
                    lo = mid + 1;
                } else {
                    hi = mid - 1;
                }
            }
        }
        return A[lo] == target ? lo : -1;
    }
}
```