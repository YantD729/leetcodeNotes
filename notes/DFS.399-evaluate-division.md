---
id: ddnf4ldpn5fv7gedeemeu1p
title: 399. Evaluate Division
desc: ''
updated: 1688126864148
created: 1688126411546
---
## #dfs #medium #union-find #seeuagain

## 解题思路

题目运用了dfs和并查集，主要就是先创造并查集，然后把他们都link到共同的祖先，如果可以link到共同的祖先就能解。

不得不说没有很懂。。。

```
class Solution {
    public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
        Map<String, String> parents = new HashMap<>();
        Map<String, Double> ratio = new HashMap<>();
        double[] res = new double[queries.size()];
        for (int i = 0; i < equations.size(); i++) {
            union(parents, ratio, equations.get(i).get(0), equations.get(i).get(1), values[i]);
        }
        for (int i = 0; i < queries.size(); i++) {
            String s1 = queries.get(i).get(0);
            String s2 = queries.get(i).get(1);
            if (!parents.containsKey(s1) || !parents.containsKey(s2) ||
                !find(parents, ratio, s1).equals(find(parents, ratio, s2)))
                res[i] = -1.0;
            else res[i] = ratio.get(s1)/ratio.get(s2);
        }
        return res;
    }

    private void union(Map<String, String> parents, Map<String, Double> ratio, String s1, String s2, double value) {
        if (!parents.containsKey(s1)) {
            parents.put(s1, s1);
            ratio.put(s1, 1.0);
        }

        if (!parents.containsKey(s2)) {
            parents.put(s2, s2);
            ratio.put(s2, 1.0);
        }

        String p1 = find(parents, ratio, s1);
        String p2 = find(parents, ratio, s2);
        parents.put(p1, p2);
        ratio.put(p1, value * ratio.get(s2)/ratio.get(s1));
    }

    private String find(Map<String, String> parent, Map<String, Double> ratio, String s) {
        if (s.equals(parent.get(s))) return s;

        String p = parent.get(s);
        String grandP = find(parent, ratio, p);
        parent.put(s, grandP);
        ratio.put(s, ratio.get(s)*ratio.get(p));
        return grandP;
    }
}

```