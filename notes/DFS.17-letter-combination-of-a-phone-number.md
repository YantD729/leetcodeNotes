---
id: q4202fsh3m34r1385fs43na
title: 17-letter-combination-of-a-phone-number
desc: ''
updated: 1688215580086
created: 1688215536849
---
## #dfs #medium #iconic

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

```
class Solution {
    String[] map = {"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    List<String> res = new ArrayList<>();
    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0) return res;
        StringBuilder sb = new StringBuilder();
        generateCom(digits, 0, sb);
        return res;
    }


    void generateCom(String digits, int idx, StringBuilder sb) {
        if (idx == digits.length()) res.add(sb.toString());
        else {
            String s = map[digits.charAt(idx) - '0'];
            for (char c : s.toCharArray()) {
                sb.append(c);
                generateCom(digits, idx + 1, sb);
                sb.deleteCharAt(sb.length() - 1);
            }
        }
    }
}
```