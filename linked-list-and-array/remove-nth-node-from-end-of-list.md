## 19. Remove Nth Node From End of List

> Given a linked list, remove thenthnode from the end of list and return its head.
>
> For example,
>
> ```
> Given linked list: 
> 1->2->3->4->5, and n = 2
>
> After removing the second node from the end, the linked list becomes 
> 1->2->3->5.
> ```
>
> **Note:**  
> Givennwill always be valid.  
> Try to do this in one pass.

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode slow = dummy;
        ListNode fast = dummy;
        for (int i = 0; i < n; i++) {
            fast = fast.next;
            if (fast == null) {
                return head;
            }
        }
        while (fast.next != null) {
            slow = slow.next;
            fast = fast.next;
        }
        slow.next = slow.next.next;
        return dummy.next;
    }
}
```



