## 98. Validate Binary Search Tree

> Given a binary tree, determine if it is a valid binary search tree \(BST\).
>
> Assume a BST is defined as follows:
>
> * The left subtree of a node contains only nodes with keys **less than **the node's key.
> * The right subtree of a node contains only nodes with keys **greater than **the node's key.
> * Both the left and right subtrees must also be binary search trees.
>
> **Example 1:**
>
> ```
>     2
>    / \
>   1   3
> ```
>
> Binary tree`[2,1,3]`, return true.
>
> **Example 2:**
>
> ```
>     1
>    / \
>   2   3
> ```
>
> Binary tree`[1,2,3]`, return false.

注意edge case只有单一节点Integer.MIN\_VALUE 或 Integer.MAX\_VALUE，所以在判断子树和父节点大小的时候要先判断子树是否为null。

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
class ResultType {
    boolean valid;
    int max;
    int min;
    public ResultType(boolean valid, int max, int min) {
        this.valid = valid;
        this.max = max;
        this.min = min;
    }
}
public class Solution {
    public boolean isValidBST(TreeNode root) {
        return helper(root).valid;
    }

    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(true, Integer.MIN_VALUE, Integer.MAX_VALUE);
        }
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        if (!left.valid || !right.valid) {
            return new ResultType(false, -1, -1);
        }
        if ((root.left != null && left.max >= root.val) || (root.right != null && right.min <= root.val)) {
            return new ResultType(false, -1, -1);
        }
        int curtMax = Math.max(right.max, root.val);
        int curtMin = Math.min(left.min, root.val);
        return new ResultType(true, curtMax, curtMin);
    }
}
```



