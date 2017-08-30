# 376. Binary Tree Path Sum

> Given a binary tree, find all paths that sum of the nodes in the path equals to a given number`target`.
>
> A valid path is from root node to any of the leaf nodes.
>
> **Example**
>
> Given a binary tree, and target =`5`:
>
> ```
>      1
>     / \
>    2   4
>   / \
>  2   3
>
> ```
>
> return
>
> ```
> [
>   [1, 2, 2],
>   [1, 4]
> ]
> ```

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

public class Solution {
    /**
     * @param root the root of binary tree
     * @param target an integer
     * @return all valid paths
     */
    public List<List<Integer>> binaryTreePathSum(TreeNode root, int target) {
        // Write your code here
        
        List<List<Integer>> results = new ArrayList();
        if(root == null) return results;
        
        List<Integer> path = new ArrayList();
        path.add(root.val);
        helper(root, root.val, target, path, results);
        return results;
    }
    
    private void helper(TreeNode node, int sum, int target, List<Integer> path, List<List<Integer>> results){
        
        if(node.left == null && node.right == null){
            
            if(sum == target){
               results.add(new ArrayList<Integer>(path));
            }
            return;
        }
        
        if(node.left != null){
            
            path.add(node.left.val);
            helper(node.left, sum + node.left.val, target, path, results);
            path.remove(path.size() - 1);
        }
        
        if(node.right != null){
            
            path.add(node.right.val);
            helper(node.right, sum + node.right.val, target, path, results);
            path.remove(path.size() - 1);
        }
    }
}
```



