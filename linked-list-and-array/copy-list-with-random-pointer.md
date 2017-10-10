## 138. Copy List with Random Pointer

> A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.
>
> Return a deep copy of the list.

关键在于建立原节点和新节点的映射关系。

1. 用HashMap建立映射关系。针对每一个节点，用dummy/tail节点来管理先后顺序（next），否则会导致while循环错乱；在每一次循环内部直接管理random的关系。
2. 用链表本身建立映射关系。第一遍循环，建立拷贝节点并且链接在原节点之后；第二遍循环，将原节点的random值赋予拷贝节点；第三遍循环，将拷贝节点拆出来；

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
 
// HashMap
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return head;
        }
        HashMap<RandomListNode, RandomListNode> map = new HashMap<RandomListNode, RandomListNode>();
        RandomListNode dummy = new RandomListNode(0);
        RandomListNode tail = dummy;
        while (head != null) {
            RandomListNode newNode;
            if (map.containsKey(head)) {
                newNode = map.get(head);
            } else {
                newNode = new RandomListNode(head.label);
                map.put(head, newNode);
            }
            if (head.random != null) {
                RandomListNode newRandom;
                if (map.containsKey(head.random)) {
                    newRandom = map.get(head.random);
                } else {
                    newRandom = new RandomListNode(head.random.label);
                    map.put(head.random, newRandom);
                }
                newNode.random = newRandom;
            }
            tail.next = newNode;
            tail = newNode;
            head = head.next;
        }
        return dummy.next;
    }
}

// Linked to itself
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return head;
        }
        RandomListNode node = head;
        while (node != null) {
            RandomListNode newNode = new RandomListNode(node.label);
            newNode.next = node.next;
            node.next = newNode;
            node = newNode.next;
        }
        node = head;
        while (node != null) {
            if (node.random != null) {
                node.next.random = node.random.next;
            }
            node = node.next.next;;
        }
        RandomListNode dummy = new RandomListNode(0);
        RandomListNode tail = dummy;
        while (head != null) {
            tail.next = head.next;
            head.next = head.next.next;
            tail = tail.next;
            head = head.next;
        }
        return dummy.next;
    }
}
```



