# 94. Binary Tree Inorder Traversal

> Given a binary tree, return theinordertraversal of its nodes' values.
>
> For example:  
> Given binary tree`[1,null,2,3]`,  
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
> return`[1,3,2]`.

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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> results = new ArrayList<Integer>();
        helper(root, results);
        return results;
    }
    
    private void helper(TreeNode root, List<Integer> results) {
        if (root == null) {
            return;
        }
        helper(root.left, results);
        results.add(root.val);
        helper(root.right, results);
    }
}

// iteration
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> results = new ArrayList<Integer>();
        if (root == null) {
            return results;
        }
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode curt = root;
        while (curt != null || !stack.isEmpty()) {
            while (curt != null) {
                stack.push(curt);
                curt = curt.left;
            }
            curt = stack.pop();
            results.add(curt.val);
            curt = curt.right;
        }
        return results;
    }
}
```



