---
id: l3xguk5t99dtaihg4r4zzi8
title: 277 Find the Celebrit
desc: ''
updated: 1688609963070
created: 1688609641017
---
## #2pointer #medium 

Suppose you are at a party with n people labeled from 0 to n - 1 and among them, there may exist one celebrity. The definition of a celebrity is that all the other n - 1 people know the celebrity, but the celebrity does not know any of them.

Now you want to find out who the celebrity is or verify that there is not one. You are only allowed to ask questions like: "Hi, A. Do you know B?" to get information about whether A knows B. You need to find out the celebrity (or verify there is not one) by asking as few questions as possible (in the asymptotic sense).

You are given a helper function bool knows(a, b) that tells you whether a knows b. Implement a function int findCelebrity(n). There will be exactly one celebrity if they are at the party.

Return the celebrity's label if there is a celebrity at the party. If there is no celebrity, return -1.

## 解题思路

其实很像brute force..第一遍先搞一个pointer，如果当前cele知道后面某个i，那就更新cele=i。

这时候不能确定的是不是第一遍loop后的cele是不是被所有人知道，或者ta知道不知道前面的人。这个时候，需要再loop一遍确认。

后面的不用检查cele知道不知道他们因为已经检查过了，只需要检查是不是每个都知道ta。

```
public class Solution extends Relation {
    public int findCelebrity(int n) {
        int cele = 0;
        for (int i = 0; i < n; i++) {
            if (knows(cele, i)) cele = i;
        }

        for (int i = 0; i < n; i++) {
            if (i < cele && knows(cele, i) || !knows(i, cele)) return -1;
            if (i > cele && !knows(i, cele)) return -1;
        }
        return cele;
    }
}
```