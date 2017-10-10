**Reverse Linked List Steps:**

* ListNode temp = post.next; 记录后一个
* post.next = prev;                  修改当前指针
* prev = post;                           移动prev
* post = temp;                          移post

**Fast/Slow快慢指针用途：**

* 判断Linked List Cycle
* 找middle节， 例如Palindrome Linked List, Quick Sort, Merge Sort
* 找倒数第n个节点， 例如Remove Nth Node From End of List

### Linked List 需要注意的问题

1. 涉及Reverse或者Delete节点导致head节点有可能被改变的题，需要预先引入dummy节点，例如Reverse Linked List II, Remove Nth Node From End of List



