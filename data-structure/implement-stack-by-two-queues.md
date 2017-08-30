# 494. Implement Stack by Two Queues

> Implement a stack by two queues. The queue is first in first out \(FIFO\). That means you can not directly pop the last element in a queue.
>
> **Example**
>
> ```
> push(1)
> pop()
> push(2)
> isEmpty() // return false
> top() // return 2
> pop()
> isEmpty() // return true
> ```

**Implement Stack by Two Queues &**

**Implement Queue by Two Stacks**

**用两个Queue，用LInkedList实现。**

* **pop\(\) : 把前面的元素全部转移到另外一个队列，poll\(\) 最后一个元素，然后再导回来**

* **top\(\): 把前面的元素转移到另外一个队列，poll\(\) 最后一个元素并记录，然后倒回来，别忘记把该元素再加回原队列，再返回。**

```java
class Stack {
    private Queue<Integer> queue1;
    private Queue<Integer> queue2;
    
    public Stack() {
        queue1 = new LinkedList<Integer>();
        queue2 = new LinkedList<Integer>();
    }
    
    // Push a new item into the stack
    public void push(int x) {
        // Write your code here
        queue1.offer(x);
    }

    // Pop the top of the stack
    public void pop() {
        // Write your code here
        while (queue1.size() > 1) {
            queue2.offer(queue1.poll());
        }
        queue1.poll();
        while (queue2.size() > 0) {
            queue1.offer(queue2.poll());
        } 
    }

    // Return the top of the stack
    public int top() {
        // Write your code here
        while (queue1.size() > 1) {
            queue2.offer(queue1.poll());
        }
        int topItem = queue1.poll();
        while (queue2.size() > 0) {
            queue1.offer(queue2.poll());
        }
        queue1.offer(topItem);
        return topItem;
    }

    // Check the stack is empty or not.
    public boolean isEmpty() {
        // Write your code here
        return queue1.isEmpty();
    }    
}
```



