---
id: d75zjuj3i2zp8ad78m9qm34
title: 232-implement-queue-using-stacks
desc: ''
updated: 1689595092303
created: 1689593629966
---
## #easy #stack 

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

void push(int x) Pushes element x to the back of the queue.
int pop() Removes the element from the front of the queue and returns it.
int peek() Returns the element at the front of the queue.
boolean empty() Returns true if the queue is empty, false otherwise.
Notes:

You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

## 解题思路

stack和queue的区别就是lifo和fifo的区别，因此对于加入东西不会像tree或者pq一样排序，加东西的时候不用太考虑。

对于pop的时候，其实是需要把第一个弄出来。这样一来就需要把顺序颠倒。两个stack互相倒来倒去可以做到这一点。

同时，stackout已然是队头，因此dump一次后并不用再dump回去，因为queue只能从队头取值。

class MyQueue {
    Stack<Integer> stackIn;
    Stack<Integer> stackOut;

    public MyQueue() {
        stackIn = new Stack<>();
        stackOut = new Stack<>();
    }
    
    public void push(int x) {
        stackIn.push(x);
    }
    
    public int pop() {
        dump();
        return stackOut.pop();
    }
    
    public int peek() {
        dump();
        return stackOut.peek();
    }
    
    public boolean empty() {
        return stackIn.isEmpty() && stackOut.isEmpty();
    }

    private void dump() {
        if (!stackOut.isEmpty()) return;
        while (!stackIn.isEmpty()) {
            stackOut.push(stackIn.pop());
        }
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
