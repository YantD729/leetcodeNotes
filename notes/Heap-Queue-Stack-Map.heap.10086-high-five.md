---
id: atcnasnvnz5rh8fszubi133
title: 10086-high-five
desc: ''
updated: 1689560721909
created: 1689560633384
---
## #easy #heap 

Given a list of the scores of different students, items, where items[i] = [IDi, scorei] represents one score from a student with IDi, calculate each student's top five average.

Return the answer as an array of pairs result, where result[j] = [IDj, topFiveAveragej] represents the student with IDj and their top five average. Sort result by IDj in increasing order.

A student's top five average is calculated by taking the sum of their top five scores and dividing it by 5 using integer division.

## 解题思路
top k -用heap，priorityQueue

但是用那个太慢了，转用hashmap sort优化

class Solution {
    private int K;
    public int[][] highFive(int[][] items) {
        Map<Integer, List<Integer>> scores = new HashMap<>();
        for (int[] it: items) {
            int id = it[0];
            int sc = it[1];
            if (!scores.containsKey(id)) scores.put(id, new ArrayList<Integer>());
            scores.get(id).add(sc);
        }

        int k = 0;
        int[][] res = new int[scores.size()][2];

        for (int id: scores.keySet()) {
            int sum = 0;
            int d = scores.get(id).size() < 5?  scores.get(id).size() : 5;
            Collections.sort(scores.get(id), Collections.reverseOrder());
            for (int i = 0; i < d; i++) {
                sum += scores.get(id).get(i);
            }
            res[k][0] = id;
            res[k][1] = sum/d;
            k++;
        }

        return res;
    }
}

###用pq的做法

class Solution {
    private int K;
    public int[][] highFive(int[][] items) {
        this.K = 5;
        TreeMap<Integer, Queue<Integer>> scores = new TreeMap<>();
        for (int[] it: items) {
            int id = it[0];
            int sc = it[1];
            if (!scores.containsKey(id)) scores.put(id, new PriorityQueue<Integer>());
            scores.get(id).add(sc);
            if (scores.get(id).size() > this.K) scores.get(id).poll();
        }

        List<int[]> res = new ArrayList<>();

        for (int id: scores.keySet()) {
            int sum = 0;
            for (int i = 0; i < this.K; i++) {
                sum += scores.get(id).poll();
            }
            res.add(new int[]{id, sum/this.K});
        }

        int[][] sol = new int[res.size()][];

        return res.toArray(sol);
    }
}