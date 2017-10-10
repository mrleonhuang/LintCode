## 599. Insert Into a Cyclic Sorted List \[LintCode\]

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

1. 如果初始节点node为null，应该用node = new ListNode\(x\)并返回, 而不是创建并返回新的变量名。
2. 循环list，判断node.val和node.next.val的关系，分小于、大于和等于三种情况考虑，每一种情况下如果x的值符合条件则插入。在等于情况下，如果循环回了start的位置，则说明list只有一个元素或者所有元素相同，则随便插入即可。

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



