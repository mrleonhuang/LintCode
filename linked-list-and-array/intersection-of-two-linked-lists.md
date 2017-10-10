## 160. Intersection of Two Linked Lists

> Write a program to find the node at which the intersection of two singly linked lists begins.
>
> For example, the following two linked lists:

> ```
> A:          a1 → a2
>                    ↘
>                      c1 → c2 → c3
>                    ↗            
> B:     b1 → b2 → b3
>
> ```
>
> begin to intersect at node c1.
>
> **Notes:**

> * If the two linked lists have no intersection at all, return
>   `null`
>   .
> * The linked lists must retain their original structure after the function returns.
> * You may assume there are no cycles anywhere in the entire linked structure.
> * Your code should preferably run in O\(n\) time and use only O\(1\) memory.

巧妙地利用Linked List Cycle的办法。**注意：链表可以允许多个节点指向同一个节点，但是同一个节点不能指向多个节点。**正因为如此，有重叠部分的两个链表相连接才会产生环。

```java
/**
 * Definition for singly-linked list.
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
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        ListNode node = headA;
        while (node.next != null) {
            node = node.next;
        }
        node.next = headB;
        ListNode cycleStart = linkedListCycle(headA);
        node.next = null;
        return cycleStart;
    }
    
    private ListNode linkedListCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;
        while (slow != fast) {
            if (fast == null || fast.next == null) {
                return null;
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        while (head != slow.next) {
            head = head.next;
            slow = slow.next;
        }
        return head;
    }
}
```



