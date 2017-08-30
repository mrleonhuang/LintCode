# 597. Subtree with Maximum Average

> Given a binary tree, find the subtree with maximum average. Return the root of the subtree.
>
> ##### Notice
>
> LintCode will print the subtree which root is your return node.  
> It's guaranteed that there is only one subtree with maximum average.
>
> **Example**
>
> Given a binary tree:
>
> ```
>      1
>    /   \
>  -5     11
>  / \   /  \
> 1   2 4    -2 
>
> ```
>
> return the node`11`.

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

class ResultType
{
    int sum; 
    int count;
    
    public ResultType(int sum, int count)
    {
        this.sum = sum;
        this.count = count;
    }
}
 
public class Solution {
    /**
     * @param root the root of binary tree
     * @return the root of the maximum average of subtree
     */
    public TreeNode maxSubtree;
    public ResultType maxResult;
     
    public TreeNode findSubtree2(TreeNode root) {
        // Write your code here
        helper(root);
        return maxSubtree;
    }
    
    private ResultType helper(TreeNode node)
    {
        if(node == null)
        {
            return new ResultType(0, 0);
        }
        
        ResultType leftResult = helper(node.left);
        ResultType rightResult = helper(node.right);
        
        int sum = leftResult.sum + rightResult.sum + node.val;
        int count = leftResult.count + rightResult.count + 1;
        ResultType result = new ResultType(sum, count);
        
        if(maxSubtree == null || maxResult.sum * count < sum * maxResult.count)
        {
           maxSubtree = node;
           maxResult = result;
        }
        
        return result;
    }
}
```



