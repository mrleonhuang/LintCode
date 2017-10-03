## 242. Convert Binary Tree to Linked Lists by Depth \[LintCode\]

> Given a binary tree, design an algorithm which creates a linked list of all the nodes at each depth \(e.g., if you have a tree with depth D, you'll have D linked lists\).
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
> return
>
> ```
> [
>   1->null,
>   2->3->null,
>   4->null
> ]
> ```

```java
// solution 1
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
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @return a lists of linked list
     */
    public List<ListNode> binaryTreeToLists(TreeNode root) {

        List<ListNode> result = new ArrayList<ListNode>();

        if(root == null){
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        int level = 1;
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                TreeNode node = queue.poll();
                ListNode listNode = new ListNode(node.val);
                if(result.size() < level){
                    result.add(listNode);
                }
                else{
                    listNode.next = result.get(level - 1);
                    result.set(level - 1, listNode);
                }

                if(node.right != null){
                    queue.offer(node.right);
                }

                if(node.left != null){
                    queue.offer(node.left);
                }
            }
            level++;
        }
        return result;
    }
}

// solution 2
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
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @return a lists of linked list
     */
    public List<ListNode> binaryTreeToLists(TreeNode root) {

        List<ListNode> result = new ArrayList<ListNode>();
        dfs(root, 1, result);
        return result;
    }

    private void dfs(TreeNode root, int level, List<ListNode> result){

        if(root == null){
            return;
        }

        ListNode listNode = new ListNode(root.val);

        if(result.size() < level){
            result.add(listNode);
        }
        else{
            listNode.next = result.get(level - 1);
            result.set(level - 1, listNode);
        }

        dfs(root.right, level + 1, result);
        dfs(root.left, level + 1, result);
    }
}
```



