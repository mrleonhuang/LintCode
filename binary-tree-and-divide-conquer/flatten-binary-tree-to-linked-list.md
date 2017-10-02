# 114. Flatten Binary Tree to Linked List

> Given a binary tree, flatten it to a linked list in-place.
>
> For example,  
> Given
>
> ```
>          1
>         / \
>        2   5
>       / \   \
>      3   4   6
>
> ```
>
> The flattened tree should look like:

> ```
>    1
>     \
>      2
>       \
>        3
>         \
>          4
>           \
>            5
>             \
>              6             
> ```

solution 1 只用返回左子树和右子树的last节点而不用返回它们的first节点，因为两个子树的first节点可以用root.left和root.right直接访问到。

solution 2中因为在flatten左子树的时候会改变root.right的值，所以要预先记录一下。

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
 
// solution 1 : Divide & Conquer
class Solution {
    public void flatten(TreeNode root) {
         helper(root);
    }
    
    private TreeNode helper(TreeNode root) {
        if (root == null) {
            return null;
        }
        TreeNode leftLast = helper(root.left);
        TreeNode rightLast = helper(root.right);
        if (leftLast != null) {
            leftLast.right = root.right;
            root.right = root.left;
            root.left = null;
        }
        if (rightLast != null) {
            return rightLast;
        }
        if (leftLast != null) {
            return leftLast;
        }
        return root;
    }
}

// solution 2: traversal
class Solution {
    private TreeNode lastNode;
    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }
        if (lastNode != null) {
            lastNode.right = root;
            lastNode.left = null;
        }
        lastNode = root;
        TreeNode right = root.right;
        flatten(root.left);
        flatten(right);
    }
}
```



