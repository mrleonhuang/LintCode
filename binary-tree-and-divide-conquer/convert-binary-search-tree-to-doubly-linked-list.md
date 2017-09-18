# 378. Convert Binary Search Tree to Doubly Linked List \[LintCode\]

> Convert a binary search tree to doubly linked list with in-order traversal.
>
> **xample**
>
> Given a binary search tree:
>
> ```
>     4
>    / \
>   2   5
>  / \
> 1   3
> ```
>
> return`1<->2<->3<->4<->5`

Divide and Conquer方法，针对每一个节点，创建DoublyListNode，并且与所返回的left分支的last节点，和right分支的first节点相连接。同时根据左右分支返回的情况，判断并返回包括当前节点的一坨分支的first和last节点是什么。总体来说就是创建节点+连接节点+返回情况。

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
 * Definition for Doubly-ListNode.
 * public class DoublyListNode {
 *     int val;
 *     DoublyListNode next, prev;
 *     DoublyListNode(int val) {
 *         this.val = val;
 *         this.next = this.prev = null;
 *     }
 * }
 */ 
class ResultType {
    DoublyListNode first;
    DoublyListNode last;
    public ResultType (DoublyListNode first, DoublyListNode last) {
        this.first = first;
        this.last = last;
    }
}
public class Solution {
    /**
     * @param root: The root of tree
     * @return: the head of doubly list node
     */
    public DoublyListNode bstToDoublyList(TreeNode root) {  
        // Write your code here
        if (root == null) {
            return null;
        }
        ResultType resultType = helper(root);
        return resultType.first;
    }

    private ResultType helper(TreeNode root) {
        if (root == null) {
            return null;
        }
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        ResultType resultType = new ResultType(null, null);
        DoublyListNode curtNode = new DoublyListNode(root.val);
        if (left == null) {
            resultType.first = curtNode;
        } else {
            left.last.next = curtNode;
            curtNode.prev = left.last;
            resultType.first = left.first;
        }
        if (right == null) {
            resultType.last = curtNode;
        } else {
            curtNode.next = right.first;
            right.first.prev = curtNode;
            resultType.last = right.last;
        }
        return resultType;
    }
}
```



