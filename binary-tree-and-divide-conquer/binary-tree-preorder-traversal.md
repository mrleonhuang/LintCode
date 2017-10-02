# 144. Binary Tree Preorder Traversal

> Given a binary tree, return thepreordertraversal of its nodes' values.
>
> For example:  
> Given binary tree`{1,#,2,3}`,  
>
>
> ```
>    1
>     \
>      2
>     /
>    3
>
> ```
>
> return`[1,2,3]`.

```java
// recursion
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> results = new ArrayList<Integer>();
        helper(root, results);
        return results;
    }
    
    private void helper(TreeNode root, List<Integer> results) {
        if (root == null) {
            return;
        }
        results.add(root.val);
        helper(root.left, results);
        helper(root.right, results);
    }
} 

// iteration
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> results = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        if (root == null) {
            return results;
        }
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode top = stack.pop();
            results.add(top.val);
            if (top.right != null) {
                stack.push(top.right);
            }
            if (top.left != null) {
                stack.push(top.left);
            }
        }
        return results;
    }
}
```



