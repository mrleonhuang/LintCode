## 86. Partition List

> Given a linked list and a valuex, partition it such that all nodes less thanxcome before nodes greater than or equal tox.
>
> You should preserve the original relative order of the nodes in each of the two partitions.
>
> For example,  
> Given`1->4->3->2->5->2`andx= 3,  
> return`1->2->2->4->3->5`.

需要check最后尾巴是否已经封上，否则会导致循环往复。比如rightTail.next = null

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
    public ListNode partition(ListNode head, int x) {
        if (head == null) {
            return head;
        }
        ListNode dummyLeft = new ListNode(0);
        ListNode leftTail = dummyLeft;
        ListNode dummyRight = new ListNode(0);
        ListNode rightTail = dummyRight;
        while (head != null) {
            if (head.val < x) {
                leftTail.next = head;
                leftTail = head;
            } else {
                rightTail.next = head;
                rightTail = head;
            }
            head = head.next;
        }
        leftTail.next = dummyRight.next;
        rightTail.next = null;
        return dummyLeft.next;
    }
}
```



