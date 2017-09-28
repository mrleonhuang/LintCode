# 474. Lowest Common Ancestor II \[LintCode\]

> Given the root and two nodes in a Binary Tree. Find the lowest common ancestor\(LCA\) of the two nodes.
>
> The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.
>
> The node has an extra attribute`parent`which point to the father of itself. The root's parent is null.
>
> **Example**
>
> For the following binary tree:
>
> ```
>   4
>  / \
> 3   7
>    / \
>   5   6
> ```
>
> LCA\(3, 5\) =`4`
>
> LCA\(5, 6\) =`7`
>
> LCA\(6, 7\) =`7`

```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public ParentTreeNode parent, left, right;
 * }
 */
public class Solution {
    /**
     * @param root: The root of the tree
     * @param A, B: Two node in the tree
     * @return: The lowest common ancestor of A and B
     */
    public ParentTreeNode lowestCommonAncestorII(ParentTreeNode root,
                                                 ParentTreeNode A,
                                                 ParentTreeNode B) {

        if(root == null || A == null || B == null) return null;
        ArrayList<ParentTreeNode> pathA = getPathToRoot(A);
        ArrayList<ParentTreeNode> pathB = getPathToRoot(B);
        ParentTreeNode LCA = null;
        int a = pathA.size() - 1;
        int b = pathB.size() - 1;
        while(a >= 0 && b >= 0) {
            if(pathA.get(a) != pathB.get(b)) {
                break;
            }
            LCA = pathA.get(a);
            a--;
            b--;
        }
        return LCA;
    }

    private ArrayList<ParentTreeNode> getPathToRoot(ParentTreeNode node) {   
        ArrayList<ParentTreeNode> path = new ArrayList();
        if(node == null) {
            return path;
        }
        while(node != null) {
           path.add(node);
           node = node.parent;
        }
        return path;
    }
}
```



