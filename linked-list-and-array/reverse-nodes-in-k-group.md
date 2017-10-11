## 25. Reverse Nodes in k-Group

> Given a linked list, reverse the nodes of a linked listkat a time and return its modified list.
>
> kis a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple ofkthen left-out nodes in the end should remain as it is.
>
> You may not alter the values in the nodes, only nodes itself may be changed.
>
> Only constant memory is allowed.
>
> For example,  
> Given this linked list:`1->2->3->4->5`
>
> For k= 2, you should return:`2->1->4->3->5`
>
> For k= 3, you should return:`3->2->1->4->5`

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode slow = dummy;
        ListNode fast = dummy;
        while (slow != null && slow.next != null) {
          for (int i = 0; i < k; i++) {
                fast = fast.next;
                if (fast == null) {
                    return dummy.next;
                }
            }
            ListNode start = slow.next;
            ListNode prev = slow;
            ListNode post = slow.next;
            for (int i = 0; i < k; i++) {
                ListNode temp = post.next;
                post.next = prev;
                prev = post;
                post = temp;
            }
            slow.next = fast;
            start.next = post;
            slow = start;
            fast = start;
        }
        return dummy.next;
    }
}
```



