---
id: pwh4gmyfhxjn28ec7sbae0o
title: 5 Longest Palindromic Substring
desc: ''
updated: 1688544492629
created: 1688544048266
---
## #2pointer #medium #iconic

Given a string s, return the longest 
palindromic substring in s.

## 解题思路

需要注意的是palindrome可以是奇数长度也可以是偶数长，所以substring有两种。

### 中心扩展法

```
class Solution {
    String palindrome(String s, int l, int r) {
        while (l >= 0 && r < s.length()
            && s.charAt(l) == s.charAt(r)){
            l--;
            r++;}
        return s.substring(l + 1, r);
    }

    public String longestPalindrome(String s) {
        String res="";
        for (int i = 0; i < s.length(); i++) {
            String s1 = palindrome(s, i, i);
            String s2 = palindrome(s, i, i + 1);
            res = res.length() > s1.length() ? res : s1;
            res = res.length() > s2.length() ? res : s2;
        }
        return res;    
    }
}
```
### 动态规划

```
Top Down
class Solution {
    
    Boolean[][] memo ;
    
    public String longestPalindrome(String s) {
        
        int len = s.length();
        
        int maxLen = 0;
        String res = "";
        memo = new Boolean[len][len];
        
        for (int left = 0; left < len; left++){
            for (int right = left; right < len; right++){
                
             if (s.charAt(left) == s.charAt(right) && isPalin(s,left + 1, right -1)){
                if (maxLen < right - left + 1) {
                    maxLen = right - left + 1;
                    res = s.substring(left, right + 1);
                    }
                }   
            }
        }
        
        return res;
    }
    
    
    public boolean isPalin(String s, int left, int right){
        
        if (left >= right){
            return true;
        }
        
        if (memo[left][right] != null){
            return memo[left][right] ;
        }
        
        if (s.charAt(left) != s.charAt(right)) {
            memo[left][right] = false;
            return memo[left][right];
        }
        
        if (right - left <= 2){
            memo[left][right] = true;
            return memo[left][right];
        }
        
        memo[left][right] = isPalin(s,left + 1, right - 1);
        return memo[left][right];
        
    }
    
}
```
#### Bottoms Up DP
```
class Solution {
    
    boolean[][] memo ;
    
    public String longestPalindrome(String s) {
        
        int len = s.length();
        
        int maxLen = 0;
        String res = "";
        memo = new boolean[len][len];
        
        for (int left = len -1; left >= 0; left--){ // notice this goes backwards
            for (int right = left; right < len; right++){
                
             if (s.charAt(left) == s.charAt(right)){
                 
                if (right - left <=2){
                    memo[left][right] = true;
                } else{
                    memo[left][right] = memo[left + 1][right - 1]; 
                }
             }
    
            if (memo[left][right]  && maxLen < right - left + 1) {
                maxLen = right - left + 1;
                res = s.substring(left, right + 1);
                }
            }   
            
        }
        
        return res;
    }
    
}

```

### Manacher 算法

```
class Solution {
    public String longestPalindrome(String s) {

        // code line +8 to line +15
        int strLen = 2 * s.length() + 3;
        char[] sChars = new char[strLen];

        /*
         * To ignore special cases at the beginning and end of the array
         * "abc" -> @ # a # b # c # $
         * "" -> @#$
         * "a" -> @ # a # $
         */
        sChars[0] = '@';
        sChars[strLen - 1] = '$';
        int t = 1;
        for (char c : s.toCharArray()) {
            sChars[t++] = '#';
            sChars[t++] = c;
        }
        sChars[t] = '#';

        int maxLen = 0;
        int start = 0;
        int maxRight = 0;
        int center = 0;
        int[] p = new int[strLen]; // i's radius, which not includes i
        for (int i = 1; i < strLen - 1; i++) {
            if (i < maxRight) {
                p[i] = Math.min(maxRight - i, p[2 * center - i]);
            }

            // expand center
            while (sChars[i + p[i] + 1] == sChars[i - p[i] - 1]) {
                p[i]++;
            }

            // update center and its bound
            if (i + p[i] > maxRight) {
                center = i;
                maxRight = i + p[i];
            }

            // update ans
            if (p[i] > maxLen) {
                start = (i - p[i] - 1) / 2;
                maxLen = p[i];
            }
        }

        return s.substring(start, start + maxLen);
    }
}
```
