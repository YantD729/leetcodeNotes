---
id: d8j77pi2o97g3ixb90h8sqt
title: 150-evaluate-reverse-polish-natation
desc: ''
updated: 1689597625628
created: 1689595182682
---
## #medium #stack #iconic

ou are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:

The valid operators are '+', '-', '*', and '/'.
Each operand may be an integer or another expression.
The division between two integers always truncates toward zero.
There will not be any division by zero.
The input represents a valid arithmetic expression in a reverse polish notation.
The answer and all the intermediate calculations can be represented in a 32-bit integer.

## 解题思路

这题首先要记住polish notation属于消消乐，所以遇到符号不用放进去，把头两个弹出即可。

class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();
        Set<String> o = new HashSet<>(Arrays.asList("+", "-", "*", "/"));
        for (String i : tokens) {
            if (!o.contains(i)) stack.push(Integer.valueOf(i));
            else {
                int a = stack.pop(), b = stack.pop();
                if (i.equals("+")) stack.push(a + b);
                else if (i.equals("-")) stack.push(b - a);
                else if (i.equals("*")) stack.push(a * b);
                else if (i.equals("/")) stack.push(b / a);
            }
        }
        return stack.peek();
    }
}