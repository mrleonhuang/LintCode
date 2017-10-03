## 619. Binary Tree Longest Consecutive Sequence III \[LintCode\]

> It's follow up problem for[`Binary Tree Longest Consecutive Sequence II`](http://www.lintcode.com/en/problem/binary-tree-longest-consecutive-sequence-ii/)
>
> Given a`k-ary tree`, find the length of the longest consecutive sequence path.  
> The path could be start and end at any node in the tree
>
> **Example**
>
> An example of test data: k-ary tree`5<6<7<>,5<>,8<>>,4<3<>,5<>,3<>>>`, denote the following structure:
>
> ```
>      5
>    /   \
>   6     4
>  /|\   /|\
> 7 5 8 3 5 3
>
> Return 5, // 3-4-5-6-7
> ```

```java
/**
 * Definition for a multi tree node.
 * public class MultiTreeNode {
 *     int val;
 *     List<TreeNode> children;
 *     MultiTreeNode(int x) { val = x; }
 * }
 */
class ResultType{

    int upCount;
    int downCount;
    int allCount;

    public ResultType(int upCount, int downCount, int allCount){
        this.upCount = upCount;
        this.downCount = downCount;
        this.allCount = allCount;
    }
}

public class Solution {
    /**
     * @param root the root of k-ary tree
     * @return the length of the longest consecutive sequence path
     */
    public int maxCount = 0;

    public int longestConsecutive3(MultiTreeNode root) {

        helper(root);
        return maxCount;
    }

    private ResultType helper(MultiTreeNode root){

        if(root == null)
            return new ResultType(0, 0, 0);

        ResultType result = new ResultType(1, 1, 1);   

        for(MultiTreeNode node : root.children){

            ResultType nodeResult = helper(node);

            if(node.val + 1 == root.val)
                result.upCount = Math.max(result.upCount, nodeResult.upCount + 1);

            if(node.val == root.val + 1)
                result.downCount = Math.max(result.downCount, nodeResult.downCount + 1);
        }

        result.allCount = Math.max(result.allCount, result.downCount + result.upCount - 1);

        int currentMax = Math.max(result.upCount, result.downCount);
        currentMax = Math.max(currentMax, result.allCount);

        if(currentMax > maxCount)
            maxCount = currentMax;

        return result;
    }
}
```



