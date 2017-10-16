**Reverse Linked List Steps:**

* ListNode temp = post.next; 记录后一个
* post.next = prev;                  修改当前指针
* prev = post;                           移动prev
* post = temp;                          移post

**Fast/Slow快慢指针用途：**

真快慢指针是前后排列，每次各走一步和两步；假快慢指针是同时指向dummy节点，快指针先走。

* 真快慢指针：判断Linked List Cycle
* 真快慢指针：找middle节点， 例如_Palindrome Linked List_, _Quick Sort_, _Merge Sort_
* 假快慢指针：找倒数第n个节点， 例如_Remove Nth Node From End of List_
* 假快慢指针：找Reverse的开始节点和结束节点，例如_Reverse Nodes in k-Group_, _Reverse Linked List II_

### Linked List 需要注意的问题

1. 涉及Reverse或者Delete节点导致head节点有可能被改变的题，需要预先引入dummy节点，例如_Reverse Linked List II_, _Remove Nth Node From End of List_
2. 需要更改链表顺序的题目要check一下最后的尾巴是否已经封上（null），例如_Partition List_



### Array需要注意的问题

1. 计算最大子集maximum subarray用当前prefixSum - minPrefixSum的方法获得
2. prefixSum数组要比原数组大一位，第0位是0，公式为prefixSum\[i\] = prefixSum\[i - 1\] + nums\[i - 1\]



