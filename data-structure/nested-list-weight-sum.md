## 551. Nested List Weight Sum \[LintCode\]

> Given a nested list of integers, return the sum of all integers in the list weighted by their depth. Each element is either an integer, or a list -- whose elements may also be integers or other lists.
>
> **Example**
>
> Given the list`[[1,1],2,[1,1]]`, return`10`. \(four 1's at depth 2, one 2 at depth 1, 4 \* 1 \* 2 + 1 \* 2 \* 1 = 10\)  
> Given the list`[1,[4,[6]]]`, return`27`. \(one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4\_2 + 6\_3 = 27\)

Solution 1: DFS: 深度优先搜索List，用HashMap记录每一个深度的Integer个数，最后HashMap里每一个深度的乘积就是结果。

Solution 2: BFS； 广度优先搜索List，每一次while循环的size就是当前depth的个数。

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer,
 *     // rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds,
 *     // if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds,
 *     // if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */

 // solution 1 DFS: 
public class Solution {
    public int depthSum(List<NestedInteger> nestedList) {
        // Write your code here
        int sum = 0;
        if (nestedList == null || nestedList.size() == 0) {
            return sum;
        }
        Map<Integer, List<Integer>> map = new HashMap<>();
        helper(nestedList, 1, map);
        for (Map.Entry<Integer, List<Integer>> entry : map.entrySet()) {
            int depth = entry.getKey();
            List<Integer> list = entry.getValue();
            int partialSum = 0;
            for (Integer number : list) {
                partialSum += (int) number;
            }
            sum += partialSum * depth;
        }
        return sum;
    }

    private void helper(List<NestedInteger> nestedList, int depth, Map<Integer, List<Integer>> map) {
        if (!map.containsKey(depth)) {
            map.put(depth, new ArrayList<Integer>());
        }
        for (NestedInteger nestedInteger: nestedList) {
            if (nestedInteger.isInteger()) {
                map.get(depth).add(nestedInteger.getInteger());
            }
            else {
                List<NestedInteger> list = nestedInteger.getList();
                helper(list, depth + 1, map);
            }
        }
    }
}

// solution 2 BFS:
public class Solution {
    public int depthSum(List<NestedInteger> nestedList) {
        // Write your code here
        int sum = 0;
        if (nestedList == null || nestedList.size() == 0) {
            return sum;
        }
        int depth = 0;
        Queue<NestedInteger> queue = new LinkedList<NestedInteger>();
        for (NestedInteger nestedInteger : nestedList) {
            queue.offer(nestedInteger);
        }
        while (!queue.isEmpty()) {
            depth++;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                NestedInteger nestedInteger = queue.poll();
                if (nestedInteger.isInteger()) {
                    sum += depth * (int) nestedInteger.getInteger();
                } else {
                    for (NestedInteger innerInteger : nestedInteger.getList()) {
                        queue.offer(innerInteger);
                    }
                }
            }
        }
        return sum;
    }
}
```



