## 92. Reverse Linked List II

> Reverse a linked list from positionmton. Do it in-place and in one-pass.
>
> For example:  
> Given`1->2->3->4->5->NULL`,m= 2 andn= 4,
>
> return`1->4->3->2->5->NULL`.
>
> **Note:**  
> Givenm,nsatisfy the following condition:  
> 1 ≤m≤n≤ length of list.

引进dummy node的目的是，如果m，n包括了head节，dummy.next指针会在操作reverse的过程中改动到改动后的头结点（参见总结中的Reverse Linked List步骤）。post指针在reverse完成之后自动指向了原postN节点。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode preM = dummy;
        ListNode nNode = dummy;
        for (int i = 1; i < m; i++) {
            preM = preM.next;
            if (preM == null) {
                return head;
            }
        }
        for (int j = 0; j < n; j++) {
            nNode = nNode.next;
            if (nNode == null) {
                return head;
            }
        }
        ListNode mNode = preM.next;
        ListNode prev = mNode;
        ListNode post = mNode.next;
        for (int k = m; k < n; k++) {
            ListNode temp = post.next;
            post.next = prev;
            prev = post;
            post = temp;
        }
        preM.next = nNode;
        mNode.next = post;
        return dummy.next;
    }
}
```



