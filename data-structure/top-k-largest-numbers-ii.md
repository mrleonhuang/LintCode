# 545. Top k Largest Numbers II

> Implement a data structure, provide two interfaces:
>
> 1. `add(number)`. Add a new number in the data structure.
> 2. `topk()`. Return the top _k _largest numbers in this data structure. _k _is given when we create the data structure.
>
> **Example**
>
> ```
> s = new Solution(3);
> >> create a new data structure.
> s.add(3)
> s.add(10)
> s.topk()
> >>return [10, 3]
> s.add(1000)
> s.add(-99)
> s.topk()
> >>return [1000, 10, 3]
> s.add(4)
> s.topk()
> >>return [1000, 10, 4]
> s.add(100)
> s.topk()
> >>return [1000, 100, 10]
> ```

**定义一个private变量maxSize记录k是多少**

**注意用Iterator的时候如果不定义Iterator&lt;Integer&gt;那么返回值将会是一个Object**

```java
public class Solution {
    
    private PriorityQueue<Integer> minHeap;
    private int maxSize;
    
    public Solution(int k) {
        // initialize your data structure here.
        minHeap = new PriorityQueue<Integer>(k + 1);
        maxSize = k;
    }

    public void add(int num) {
        // Write your code here
        minHeap.offer(num);
        if (minHeap.size() > maxSize) {
            minHeap.poll();
        }
    }

    public List<Integer> topk() {
        // Write your code here
        List<Integer> results = new ArrayList<Integer>();
        Iterator it = minHeap.iterator();
        while (it.hasNext()) {
            results.add((Integer) it.next());
        }
        Collections.sort(results, Collections.reverseOrder());
        return results;
    }
};
```



