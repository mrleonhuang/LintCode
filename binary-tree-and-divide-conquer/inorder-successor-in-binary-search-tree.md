## 448. Inorder Successor in Binary Search Tree \[LintCode\]

> Given a binary search tree \([See Definition](http://www.lintcode.com/problem/validate-binary-search-tree/)\) and a node in it, find the in-order successor of that node in the BST.
>
> If the given node has no in-order successor in the tree, return`null`.
>
> ##### Notice
>
> It's guaranteed\_p\_is one node in the given tree. \(You can directly compare the memory address to find p\)
>
> **Example**
>
> Given tree =`[2,1]`and node =`1`:
>
> ```
>   2
>  /
> 1
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
> ```
>
> return node`3`.

第一个while循环是在利用BST的特性从原始节点（root of tree）去寻找p点所在的位置，基于中序遍历的特性，如果所找的p在左边，则用successor变量记录当前节点为左子树的后续节点。

找到p点之后，根据中序遍历的特性，去寻找下一个节点所在位置：如果p有右子树则successor为右子树的左下角元素；如果p没有右子树则successor为上面所记载的successor。

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
        while(root != null && root.val != p.val) {
            if (p.val < root.val) {
                successor = root;
                root = root.left;
            }
            if (root.val < p.val) {
                root = root.right;
            }
        }
        if (root == null) {
            return null;
        }
        if (root.right == null) {
            return successor;
        }
        root = root.right;
        while (root.left != null) {
            root = root.left;
        }
        return root;
    }
}
```



