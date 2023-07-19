---
id: zpwojy2q8tylm8cco318aqa
title: 341-flatten-nested-list-iterator
desc: ''
updated: 1687271845470
created: 1687271719084
---
# 341. Flattern Nested List Iterator

## #dfs #medium #ood

You are given a nested list of integers nestedList. Each element is either an integer or a list whose elements may also be integers or other lists. Implement an iterator to flatten it.

Implement the NestedIterator class:

NestedIterator(List<NestedInteger> nestedList) Initializes the iterator with the nested list nestedList.
int next() Returns the next integer in the nested list.
boolean hasNext() Returns true if there are still some integers in the nested list and false otherwise.

```
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return empty list if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class NestedIterator implements Iterator<Integer> {
    List<Integer> flattenList = null;
    int current = 0;
    public NestedIterator(List<NestedInteger> nestedList) {
        flattenList = new ArrayList<>();
        for(NestedInteger integer: nestedList){
            helper(integer);
        }
    }

    @Override
    public Integer next() {
        return flattenList.get(current++);
    }

    @Override
    public boolean hasNext() {
        return current<flattenList.size();
    }

    public void helper(NestedInteger value){
        if(value.isInteger()){
            flattenList.add(value.getInteger());
        } else {
            for(NestedInteger integer: value.getList()){
                helper(integer);
            }
        }
    }
}

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i = new NestedIterator(nestedList);
 * while (i.hasNext()) v[f()] = i.next();
 */
```