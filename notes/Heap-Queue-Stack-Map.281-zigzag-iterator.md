---
id: 43imj853jlio1qubgxky3z3
title: 281-zigzag-iterator
desc: ''
updated: 1688968345847
created: 1688956234698
---
## #hqsm #medium #ood

Given two vectors of integers v1 and v2, implement an iterator to return their elements alternately.

Implement the ZigzagIterator class:

ZigzagIterator(List<int> v1, List<int> v2) initializes the object with the two vectors v1 and v2.
boolean hasNext() returns true if the iterator still has elements, and false otherwise.
int next() returns the current element of the iterator and moves the iterator to the next element.


这个解法还蛮有趣的，其实算是brute force。
```
public class ZigzagIterator {
    int i1 = 0;
    int i2 = 0;
    
    boolean flag = false;
    
    List<Integer> l1;
    List<Integer> l2;
    
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        l1 = v1;
        l2 = v2;
    }

    public int next() {
        flag = !flag;
        
        if (i1 < l1.size() && (flag  || i2 >= l2.size())) 
            return l1.get(i1++);
            
        if (i2 < l2.size() && (!flag || i1 >= l1.size())) 
            return l2.get(i2++);
        
        return -1;
    }

    public boolean hasNext() {
        return i1 < l1.size() || i2 < l2.size();
    }
}
```