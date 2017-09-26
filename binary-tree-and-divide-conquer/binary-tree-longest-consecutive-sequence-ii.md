# 614. Binary Tree Longest Consecutive Sequence II \[LintCode\]

> Given a binary tree, find the length of the longest consecutive sequence path.
>
> The path could be start and end at any node in the tree
>
> **Example**
>
> ```
>     1
>    / \
>   2   0
>  /
> 3
> ```
>
> Return`4`//`0-1-2-3`

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class ResultType{

    public int downCount;
    public int upCount;
    public int allCount;

    public ResultType(int downCount, int upCount, int allCount){
        this.downCount = downCount;
        this.upCount = upCount;
        this.allCount = allCount;
    }
} 

public class Solution {
    /**
     * @param root the root of binary tree
     * @return the length of the longest consecutive sequence path
     */
    public int maxCount = 0; 

    public int longestConsecutive2(TreeNode root) {
        helper(root);
        return maxCount;
    }

    private ResultType helper(TreeNode node) {
        if(node == null) 
            return new ResultType(0, 0, 0);

        ResultType left = helper(node.left);
        ResultType right = helper(node.right);
        ResultType result = new ResultType(1, 1, 1);
        if (node.left != null) {
            if(node.left.val  == node.val + 1){
                result.downCount = Math.max(result.downCount, left.downCount + 1);
            }
            if(node.left.val + 1 == node.val){
                result.upCount = Math.max(result.upCount, left.upCount + 1);
            }
        }
        if (node.right != null) {
            if (node.right.val  == node.val + 1) {
                result.downCount = Math.max(result.downCount, right.downCount + 1);
            }
            if (node.right.val + 1 == node.val) {
                result.upCount = Math.max(result.upCount, right.upCount + 1);
            }
        }
        if (node.left != null && node.right != null) {
            if (node.val + 1 == node.left.val && node.right.val + 1 == node.val) {
                result.allCount = Math.max(result.allCount, left.downCount + 1 + right.upCount);
            }
            if (node.val == node.left.val + 1 && node.right.val == node.val + 1) {
                result.allCount = Math.max(result.allCount, left.upCount + 1 + right.downCount);
            }
        }
        int currentMax = Math.max(Math.max(result.upCount, result.downCount), result.allCount);
        if (currentMax > maxCount) {
            maxCount = currentMax;
        }
        return result;
    }
}
```



