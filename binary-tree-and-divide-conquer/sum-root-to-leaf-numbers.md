# 129. Sum Root to Leaf Numbers \[LeetCode\]

> Given a binary tree containing digits from`0-9`only, each root-to-leaf path could represent a number.
>
> An example is the root-to-leaf path`1->2->3`which represents the number`123`.
>
> Find the total sum of all root-to-leaf numbers.
>
> For example,
>
> ```
>     1
>    / \
>   2   3
>
> ```
>
> The root-to-leaf path`1->2`represents the number`12`.  
> The root-to-leaf path`1->3`represents the number`13`.
>
> Return the sum = 12 + 13 =`25`.

笨办法：DFS得出所有路径统一相加

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
class Solution {
    public int sumNumbers(TreeNode root) {
        List<List<Integer>> paths = new ArrayList<>();
        List<Integer> path = new ArrayList<Integer>();
        dfs(root, path, paths);
        int sum = 0;
        for (List<Integer> way : paths) {
            int mult = 1;
            int curtSum = 0;
            for (int i = way.size() - 1; i >= 0; i--) {
                curtSum += way.get(i) * mult;
                mult *= 10;
            }
            sum += curtSum;
        }
        return sum;
    }
    
    private void dfs(TreeNode node, List<Integer> path, List<List<Integer>> paths) {
        if (node == null) {
            return;
        }
        path.add(node.val);
        if (node.left == null && node.right == null) {
            paths.add(new ArrayList<Integer>(path));
        }
        dfs(node.left, path, paths);
        dfs(node.right, path, paths);
        path.remove(path.size() - 1);
    }
}
```

Divide & Conquer：通过参数sum向下传递本节点以上的值是什么，通过return的值向上返回本节点以下的相加和

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
class Solution {
    public int sumNumbers(TreeNode root) {
        return getSum(root, 0);
    }
    
    private int getSum(TreeNode node, int sum) {
        if (node == null) {
            return 0;
        }
        if (node.left == null && node.right == null) {
            return sum * 10 + node.val;
        }
        int leftSum = getSum(node.left, sum * 10 + node.val);
        int rightSum = getSum(node.right, sum * 10 + node.val);
        return leftSum + rightSum;
    }
}
```



