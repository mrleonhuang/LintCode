**Reverse Linked List Steps:**

* ListNode temp = post.next; 记录后一个
* post.next = prev;                  修改当前指针
* prev = post;                           移动prev
* post = temp;                          移post



**Fast/Slow快慢指针用途：**

真快慢指针是前后排列，每次各走一步和两步；假快慢指针是同时指向dummy节点，快指针先走。

* 真快慢指针：判断Linked List Cycle
* 真快慢指针：找middle节点， 例如Palindrome Linked List, Quick Sort, Merge Sort
* 假快慢指针：找倒数第n个节点， 例如Remove Nth Node From End of List
* 假快慢指针：找Reverse的开始节点和结束节点，例如Reverse Nodes in k-Group, Reverse Linked List II

### Linked List 需要注意的问题

1. 涉及Reverse或者Delete节点导致head节点有可能被改变的题，需要预先引入dummy节点，例如Reverse Linked List II, Remove Nth Node From End of List
2. 需要更改链表顺序的题目要check一下最后的尾巴是否已经封上（null），例如Partition List



