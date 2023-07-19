---
id: quim2qeuc7h81w7cet9kklm
title: 155-min-stack
desc: ''
updated: 1689248740939
created: 1689247959210
---
## #medium #stack #ood

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class:

MinStack() initializes the stack object.
void push(int val) pushes the element val onto the stack.
void pop() removes the element on the top of the stack.
int top() gets the top element of the stack.
int getMin() retrieves the minimum element in the stack.
You must implement a solution with O(1) time complexity for each function.
## 解题思路

主要是这个好像唯一一个特殊要求就是找到min啊。。所以找一个记录最小值的就行，其余照常。

class MinStack {
    Stack<Integer> st;
    Stack<Integer> stMin;
    public MinStack() {
       st = new Stack<>();
       stMin = new Stack<>();
    }
    
    public void push(int val) {
        st.push(val);
        if (val < stMin.peek())
            stMin.push(val);
    }
    
    public void pop() {
       int pop = st.pop();
       if (pop == stMin.peek())
        stMin.pop;
    }
    
    public int top() {
        return st.peek();
    }
    
    public int getMin() {
        return stMin.peek();
    }
}
