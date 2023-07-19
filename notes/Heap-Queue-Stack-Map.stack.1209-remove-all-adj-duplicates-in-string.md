---
id: 2tni9q70whijqoyfb9rb2g3
title: 1209-remove-all-adj-duplicates-in-string
desc: ''
updated: 1689299458843
created: 1689257133433
---
## #medium #deque 

You are given a string s and an integer k, a k duplicate removal consists of choosing k adjacent and equal letters from s and removing them, causing the left and the right side of the deleted substring to concatenate together.

We repeatedly make k duplicate removals on s until we no longer can.

Return the final string after all such duplicate removals have been made. It is guaranteed that the answer is unique.

class Solution {
    class Adj {
        char ch;
        int freq;
        public Adj(char ch, int freq) {
            this.ch = ch;
            this.freq = freq;
        }
    }
    public String removeDuplicates(String s, int k) {
        ArrayDeque<Adj> st = new ArrayDeque<Adj>();
        
        for (char c: s.toCharArray()) {
            if (!st.isEmpty() && st.peekLast().ch == c) {
                st.peekLast().freq++;
            } else st.addLast(new Adj(c, 1));
            if (st.peekLast().freq == k) 
                st.removeLast();
        }

        StringBuilder sb = new StringBuilder();
        for (Adj adj: st) {
            sb.append(String.valueOf(adj.ch).repeat(adj.freq));
        }
        return sb.toString();
    }
}

public String removeDuplicates(String s, int k) {
    StringBuilder sb = new StringBuilder(s);
    Stack<Integer> counts = new Stack<>();
    for (int i = 0; i < sb.length(); ++i) {
        if (i == 0 || sb.charAt(i) != sb.charAt(i - 1)) {
            counts.push(1);
        } else {
            int incremented = counts.pop() + 1;
            if (incremented == k) {
                sb.delete(i - k + 1, i + 1);
                i = i - k;
            } else {
                counts.push(incremented);
            }
        }
    }
    return sb.toString();
}