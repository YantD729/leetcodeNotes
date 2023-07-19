---
id: x65thecv7ciygu2yo9gxvwn
title: 362-design-hit-counter
desc: ''
updated: 1688968534976
created: 1688968367867
---
## #hqsm #medium #iconic

Design a hit counter which counts the number of hits received in the past 5 minutes (i.e., the past 300 seconds).

Your system should accept a timestamp parameter (in seconds granularity), and you may assume that calls are being made to the system in chronological order (i.e., timestamp is monotonically increasing). Several hits may arrive roughly at the same time.

Implement the HitCounter class:

HitCounter() Initializes the object of the hit counter system.
void hit(int timestamp) Records a hit that happened at timestamp (in seconds). Several hits may happen at the same timestamp.
int getHits(int timestamp) Returns the number of hits in the past 5 minutes from timestamp (i.e., the past 300 seconds).

## 解题思路

就是记录hits的一个东西，然后超过时间范围的部分就poll掉。

考fifo

```
class HitCounter {
    Queue<Integer> hits;
    public HitCounter() {
        hits = new LinkedList<>();
    }
    
    public void hit(int timestamp) {
        hits.offer(timestamp);
    }
    
    public int getHits(int timestamp) {
        while (hits.size() > 0 && (timestamp - hits.peek() >= 300)) {
            hits.poll();
        }
        return hits.size();
    }
}
```