# 595. Binary Tree Longest Consecutive Sequence \[LintCode\]

> Given a binary tree, find the length of the longest consecutive sequence path.
>
> The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child \(`cannot be the reverse`\).
>
> **Example**
>
> For example,
>
> ```
>    1
>     \
>      3
>     / \
>    2   4
>         \
>          5
> ```
>
> Longest consecutive sequence path is`3-4-5`, so return`3`.
>
> ```
>    2
>     \
>      3
>     / 
>    2    
>   / 
>  1
> ```
>
> Longest consecutive sequence path is`2-3`,not`3-2-1`, so return`2`.

solution 3 是从 246. Binary Tree Path Sum II \[LintCode\] 中学到的traversal的方法“buffer回看法”。

```java
// solution 1
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
    /**
     * @param root the root of binary tree
     * @return the length of the longest consecutive sequence path
     */
    public int maxCount = 0;

    public int longestConsecutive(TreeNode root) {
        helper(root);
        return maxCount;
    }

    private int helper(TreeNode node){
        if(node == null) {
            return 0;
        }
        int left = helper(node.left);
        int right = helper(node.right);
        int subtreeMax = 1;
        if(node.left != null && node.left.val == node.val + 1) {
            subtreeMax = Math.max(subtreeMax, left + 1);
        }
        if(node.right != null && node.right.val == node.val + 1) {
            subtreeMax = Math.max(subtreeMax, right + 1);
        }
        if(subtreeMax > maxCount) {
            maxCount = subtreeMax;
        }
        return subtreeMax;
    }
}

// solution 2
public class Solution {
    /**
     * @param root the root of binary tree
     * @return the length of the longest consecutive sequence path
     */

    public int longestConsecutive(TreeNode root) {
        return helper(root, null, 0);
    }

    private int helper(TreeNode root, TreeNode parent, int lengthWithoutRoot) {
        if (root == null) {
            return 0;
        }
        int length = (parent != null && parent.val + 1 == root.val)
            ? lengthWithoutRoot + 1
            : 1;
        int left = helper(root.left, root, length);
        int right = helper(root.right, root, length);
        return Math.max(length, Math.max(left, right));
    }
}

// solution 3
class Solution {
    private int maxCount;
    public int longestConsecutive(TreeNode root) {
        this.maxCount = 0;
        List<Integer> buffer = new ArrayList<Integer>();
        helper(root, buffer);
        return this.maxCount;
    }
    
    private void helper(TreeNode node, List<Integer> buffer) {
        if (node == null) {
            return;
        }
        buffer.add(node.val);
        int count = 1;
        for (int i = buffer.size() - 1; i > 0; i--) {
          if (buffer.get(i) != buffer.get(i - 1) + 1) {
            break;
          } 
          count++;
        }
        this.maxCount = Math.max(this.maxCount, count);
        helper(node.left, buffer);
        helper(node.right, buffer);
        buffer.remove(buffer.size() - 1);
  }
}
```



