## 142. Linked List Cycle II

> Given a linked list, return the node where the cycle begins. If there is no cycle, return`null`.
>
> **Note:**Do not modify the linked list.
>
> **Follow up**:  
> Can you solve it without using extra space?

当快慢指针相遇后，头节点和slow节点一次走一步，**一直到head == slow.next而不是head == slow !!**

证明：假设head到环开始节点的距离为A，环的周长为C，在环中L的位置相遇：

则快指针走的距离是慢指针的2倍，所以

S = A + L

2S = A +L + C\(或者n倍C）

代入之后可得A = C - L

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null) {
            return head;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while (slow != fast) {
            if (fast == null || fast.next == null) {
                return null;
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        while (slow.next != head) {
            head = head.next;
            slow = slow.next;
        }
        return head;
    }
}
```



