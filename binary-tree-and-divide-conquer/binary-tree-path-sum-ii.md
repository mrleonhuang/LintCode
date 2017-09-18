# 246. Binary Tree Path Sum II \[LintCode\]

> Your are given a binary tree in which each node contains a value. Design an algorithm to get all paths which sum to a given value. The path does not need to start or end at the root or a leaf, but it must go in a straight line down.
>
> **Example**
>
> Given a binary tree:
>
> ```
>     1
>    / \
>   2   3
>  /   /
> 4   2
> ```
>
> for target =`6`, return
>
> ```
> [
>   [2, 4],
>   [1, 3, 2]
> ]
> ```

针对DFS的每一步到达的节点，从当前节点往前一直到根节点，去找”截止到当前节点等于target的序列“，每找到一个就创建一个子序列。DFS函数中用level来标记当前的层数，好从buffer里找到对应的value。

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
    public List<List<Integer>> binaryTreePathSum2(TreeNode root, int target) {
        // Write your code here
        List<List<Integer>> results = new ArrayList<>();
        List<Integer> buffer = new ArrayList<Integer>();
        dfs(root, target, buffer, 0, results);
        return results;
    }

    private void dfs(TreeNode root, int target, List<Integer> buffer, int level, List<List<Integer>> results) {
        if (root == null) {
            return;
        }        
        buffer.add(root.val);
        int sum = target;
        for (int i = level; i >= 0; i--) {
            sum -= buffer.get(i);
            if (sum == 0) {
                List<Integer> path = new ArrayList<Integer>();
                for (int j = i; j <= level; j++) {
                    path.add(buffer.get(j));
                }
                results.add(path);
            }
        }
        dfs(root.left, target, buffer, level + 1, results);
        dfs(root.right, target, buffer, level + 1, results);
        buffer.remove(buffer.size() - 1);
    }
}
```



