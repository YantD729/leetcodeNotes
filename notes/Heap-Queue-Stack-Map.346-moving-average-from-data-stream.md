---
id: qhgijwfmbypc9vyir4iqu0l
title: 346-moving-average-from-data-stream
desc: ''
updated: 1688954365316
created: 1688953901157
---
## #hqsm #easy #ood

Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

Implement the MovingAverage class:

MovingAverage(int size) Initializes the object with the size of the window size.
double next(int val) Returns the moving average of the last size values of the stream.

## 解题思路

因为我们只需要keep后n个数字，所以我们完全可以逐步更新，不用每次都for loop。

另一个需要注意的是，在next那一步，当size >= window的时候，需要offer再poll值，然后sum既需要减也需要加。

最后return的时候，需要除(1.0 * size)不然结果不是double。

```
class MovingAverage {
    private int windowSize;
    LinkedList<Integer> nums;
    long currSum;
    public MovingAverage(int size) {
        windowSize = size;
        nums = new LinkedList<>();
        currSum = 0;
    }
    
    public double next(int val) {
        if (nums.size() < windowSize) {
            nums.offer(val);
            currSum += val;
            return currSum / (1.0 * nums.size());
        } else {
            nums.offer(val);
            currSum += val;
            currSum -= nums.poll();
            return currSum/(1.0 * windowSize);
        }
        
    }
}

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param_1 = obj.next(val);
 */
```
