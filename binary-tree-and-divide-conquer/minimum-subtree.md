# 596. Minimum Subtree

> Given a binary tree, find the subtree with minimum sum. Return the root of the subtree.
>
> ##### Notice
>
> LintCode will print the subtree which root is your return node.  
> It's guaranteed that there is only one subtree with minimum sum and the given binary tree is not an empty tree.
>
> **Example**
>
> Given a binary tree:
>
> ```
>      1
>    /   \
>  -5     2
>  / \   /  \
> 0   2 -4  -5 
>
> ```
>
> return the node`1`.

```java
// solution 1
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
class ResultType {
    public TreeNode minSubtree;
    public int sum, minSum;
    public ResultType(TreeNode minSubtree, int minSum, int sum) {
        this.minSubtree = minSubtree;
        this.minSum = minSum;
        this.sum = sum;
    }
}
 
public class Solution {
    /**
     * @param root the root of binary tree
     * @return the root of the minimum subtree
     */
     
    public TreeNode findSubtree(TreeNode root) {
        ResultType result = helper(root);
        return result.minSubtree;
    }
    
    public ResultType helper(TreeNode node) {
        
        if (node == null) {
            return new ResultType(null, Integer.MAX_VALUE, 0);
        }
        
        ResultType leftResult = helper(node.left);
        ResultType rightResult = helper(node.right);
        
        ResultType result = new ResultType(
            node,
            leftResult.sum + rightResult.sum + node.val,
            leftResult.sum + rightResult.sum + node.val
        );
        
        if (leftResult.minSum < result.minSum) {
            result.minSum = leftResult.minSum;
            result.minSubtree = leftResult.minSubtree;
        }
        
        if (rightResult.minSum < result.minSum) {
            result.minSum = rightResult.minSum;
            result.minSubtree = rightResult.minSubtree;
        }
        
        return result;
    }
}

// solution 2
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
public class Solution {
    /**
     * @param root the root of binary tree
     * @return the root of the minimum subtree
     */
    public TreeNode minSubtree;
    public int minSum = Integer.MAX_VALUE;
     
    public TreeNode findSubtree(TreeNode root) {
        // Write your code here
        getSum(root);
        return minSubtree;
    }
    
    private int getSum(TreeNode node)
    {
        if(node == null) return 0;
        
        int sum = getSum(node.left) + getSum(node.right) + node.val;
        
        if(sum < minSum)
        {
            minSubtree = node;
            minSum = sum;
        }
        
        return sum;
    }
}
```



