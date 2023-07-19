---
id: 5lb8i43nueuo39wfmhgu5b0
title: 20-valid-parentheses
desc: ''
updated: 1689601031286
created: 1689598930569
---
## #easy #iconic

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.


## 解题思路

就是valid括号必须要对着，这个版本就是遇到左括号推进stack，右括号pop，就完事。
利用了括号要对着的对称性，以及stack lifo的特性。

这种可以和最后一个对着的，就考虑lifo

class Solution {
    public boolean isValid(String s) {
        char[] chars = s.toCharArray();
        Stack<Character> stack = new Stack<>();

        for (char elem: chars) {
            if (elem == '(' || elem == '[' || elem == '{') {
                stack.push(elem);
                continue;
            } else if (stack.empty()) return false;

            char top = stack.pop();

            if (top == '(' && elem != ')') return false;
            if (top == '{' && elem != '}') return false;
            if (top == '[' && elem != ']') return false;
        }

        return stack.empty();
    }
}