---
id: b0aw2qib9k1ahscprnh19s5
title: 1249-min-remove-to-make-valid-parentheses
desc: ''
updated: 1689256652839
created: 1689256478215
---
## #medium #stack #parentheses

Given a string s of '(' , ')' and lowercase English characters.

Your task is to remove the minimum number of parentheses ( '(' or ')', in any positions ) so that the resulting parentheses string is valid and return any valid string.

Formally, a parentheses string is valid if and only if:

It is the empty string, contains only lowercase characters, or
It can be written as AB (A concatenated with B), where A and B are valid strings, or
It can be written as (A), where A is a valid string.

## 解题思路

为什么stack的题目都可以转化成array做？

记得第二次遍历`(`的时候一定是从右往左，因为它是从右舵出来的。其实open起到了类似stack的计数作用。

class Solution {
    public String minRemoveToMakeValid(String s) {
        char[] arr = s.toCharArray();
        int open = 0;

        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == '(') open++;
            if (arr[i] == ')') {
                if (open == 0) arr[i] = '*';
                else open--;
            }
        }

        for (int i = arr.length - 1; i >= 0; i--) {
            if (arr[i] == '(' && open != 0) {
                open--;
                arr[i] = '*';
            }
        }

        StringBuilder sb = new StringBuilder();
        for (char c : arr) {
            if (c != '*') sb.append(c);
        }
        return sb.toString();
    }
}

记录一个stack做法：
class Solution {
    public String minRemoveToMakeValid(String s) {
        char[] arr = s.toCharArray();
        Stack<Integer> stack = new Stack<Integer>();
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < arr.length; i++){   //n
            if (arr[i] == '('){
                stack.push(i);
            }
            else if (arr[i] == ')'){
                if (stack.size() > 0){
                    stack.pop();
                }
                else {
                    arr[i] = ' ';
                }
            }
        }
        while (stack.size() > 0){       //worst case n
            arr[stack.pop()] = ' ';
        }

        for (char ch: arr){     // wost cast n
            if (ch != ' ') sb.append(ch);
        }

        return sb.toString();
    }
}
//Complexity: n + n + n = O(n)