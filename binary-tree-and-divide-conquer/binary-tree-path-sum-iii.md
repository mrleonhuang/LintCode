# 472. Binary Tree Path Sum III \[LintCode\]

> Give a binary tree, and a target number, find all path that the sum of nodes equal to target, the path could be start and end at any node in the tree.
>
> **Example**
>
> Given binary tree:
>
> ```
>     1
>    / \
>   2   3
>  /
> 4
> ```
>
> and target =`6`. Return :
>
> ```
> [
>   [2, 4],
>   [2, 1, 3],
>   [3, 1, 2],
>   [4, 2]
> ]
> ```

DFS遍历嵌套DFS搜索，第一层DFS只用于移动（遍历），第二层是从当前根节点出发，往3个方向分别深度优先去搜索。

易错点：

* 为了避免重复，设置from节点来标记当前搜索方向

* 有可能有负数节点，因此当target为0的时候要继续搜索，搜索的出口为死胡同（叶子节点）

```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public int val;
 *     public ParentTreeNode parent, left, right;
 * }
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @param target an integer
     * @return all valid paths
     */
    public List<List<Integer>> binaryTreePathSum3(ParentTreeNode root, int target) {
        // Write your code here
        List<List<Integer>> results = new ArrayList<>();
        dfs(root, target, results);
        return results;
    }

    private void dfs(ParentTreeNode root, int target, List<List<Integer>> results) {
        if (root == null) {
            return;
        }
        List<Integer> path = new ArrayList<Integer>();
        findSum(root, null, target, path, results);
        dfs(root.left, target, results);
        dfs(root.right, target, results);
    }

    private void findSum(ParentTreeNode root, 
                         ParentTreeNode from, 
                         int target, 
                         List<Integer> path, 
                         List<List<Integer>> results) {
        path.add(root.val);
        target = target - root.val;
        if (target == 0) {
            results.add(new ArrayList<Integer>(path));
        }  
        if (root.parent != null && root.parent != from) {
            findSum(root.parent, root, target, path, results);
        }
        if (root.left != null && root.left != from) {
            findSum(root.left, root, target, path, results);
        }
        if (root.right != null && root.right != from) {
            findSum(root.right, root, target, path, results);
        }
        path.remove(path.size() - 1);
    }
}
```



