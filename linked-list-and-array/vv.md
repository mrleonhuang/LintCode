# 599. Insert Into a Cyclic Sorted List

> Given a node from a cyclic linked list which has been sorted, write a function to insert a value into the list such that it remains a cyclic sorted list. The given node can be any single node in the list. Return the inserted new node.
>
> ##### Notice
>
> `3->5->1`is a cyclic list, so`3`is next node of`1`.  
> `3->5->1`is same with`5->1->3`
>
> **Example**
>
> Given a list, and insert a value`4`:  
> `3->5->1`  
> Return`5->1->3->4`

```java
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param node a list node in the list
     * @param x an integer
     * @return the inserted new list node
     */
    public ListNode insert(ListNode node, int x) {
        // Write your code here
        if (node == null) {
            node = new ListNode(x);
            node.next = node;
            return node;
        }
        ListNode startNode = node;
        while (node != null && node.next != null) {
            if (node.val < node.next.val) {
                if (node.val <= x && x <= node.next.val) {
                    return insertNode(node, x);
                }    
            } else if (node.val > node.next.val) {
                if (x >= node.val || x <= node.next.val) {
                    return insertNode(node, x);
                }
            } else {
                if (node.next == startNode) {
                    return insertNode(node, x);
                }
            }
            node = node.next;
        }
        return null;
    }
    
    private ListNode insertNode(ListNode node, int x) {
        ListNode newNode = new ListNode(x);
        newNode.next = node.next;
        node.next = newNode;
        return newNode;
    }
}
```









