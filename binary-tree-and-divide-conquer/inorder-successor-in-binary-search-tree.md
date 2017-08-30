# 448. Inorder Successor in Binary Search Tree

> Given a binary search tree \([See Definition](http://www.lintcode.com/problem/validate-binary-search-tree/)\) and a node in it, find the in-order successor of that node in the BST.
>
> If the given node has no in-order successor in the tree, return`null`.
>
> ##### Notice
>
> It's guaranteed_p_is one node in the given tree. \(You can directly compare the memory address to find p\)
>
> **Example**
>
> Given tree =`[2,1]`and node =`1`:
>
> ```
>   2
>  /
> 1
>
> ```
>
> return node`2`.
>
> Given tree =`[2,1,3]`and node =`2`:
>
> ```
>   2
>  / \
> 1   3
>
> ```
>
> return node`3`.

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
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        
        TreeNode successor = null;
        
        while(root != null && root.val != p.val){
            
            if(p.val < root.val){
                successor = root;
                root = root.left;
            }
            
            if(root.val < p.val){
                root = root.right;
            }
        }
        
        if(root == null)
            return null;
            
        if(root.right == null)
            return successor;
        
        root = root.right;
        
        while(root.left != null){
            root = root.left;
        }
        
        return root;
    }
}
```



