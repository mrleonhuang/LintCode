**Reverse Linked List Steps:**

* ListNode temp = post.next; 记录后一个
* post.next = prev;                  修改当前指针
* prev = post;                           移动prev
* post = temp;                          移post

  


