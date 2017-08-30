# 621. Maximum Subarray V

> Given an integer arrays, find a contiguous subarray which has the largest sum and length should be between`k1`and`k2`\(include k1 and k2\).  
> Return the largest sum, return 0 if there are fewer than k1 elements in the array.
>
> ##### Notice
>
> Ensure that the result is an integer type.
>
> **Example**
>
> Given the array`[-2,2,-3,4,-1,2,1,-5,3]`and k1 =`2`, k2 =`4`, the contiguous subarray`[4,-1,2,1]`has the largest sum =`6`.

**思想和Maximum Subarray IV类似但是限定了k1到k2范围。因为当循环遍历到比k2大的节点的时候，找minPrefix的范围是变化的 - 前面少一个数，后面多一个数。**

**刚开始到每个节点的时候，子循环从 i - k2开始一直到 i - k1，用minPrefix变量去找最小值，复杂度太高，内存超了。**

**答案1：新的思想（单调队列），用一个linkedList来维护一个queue，每次 i 变化的时候**

* **当 k1 &lt;= i && i &lt;= k2的时候，将当前 i - k1加入进来，队列中从尾巴开始把所有大于当前 i - k1的元素用getLast（）删除掉，把 i - k1元素放进队尾，最小的元素在队头。**

* **当 i &gt; k2的时候，除了上面的操作还要用getFirst\(\)裁剪掉 i - k2之前的元素， 从而保证了队列中的元素就是可以作为minPrefix的元素范围，并且最小的元素在队头。**

  **相当于人肉构造PriorityQueue。**

**答案2：用PriorityQueue&lt;Pair&gt;，Pair有sum和index属性，当 i &gt;k2的时候，每次出列的元素要检查index是否小于 i - k1。**

```java
// Solution 1
public class Solution {
    /**
     * @param nums an array of integers
     * @param k1 an integer
     * @param k2 an integer
     * @return the largest sum
     */
    public int maxSubarray5(int[] nums, int k1, int k2) {
        // Write your code here
      if (nums == null || nums.length == 0 || nums.length < k1) {
        return 0;
      }
      int largestSum = Integer.MIN_VALUE;
      int[] sums = new int[nums.length + 1];
      sums[0] = 0;
      LinkedList<Integer> queue = new LinkedList<Integer>();
      for (int i = 1; i <= nums.length; i++) {
        sums[i] = sums[i - 1] + nums[i - 1];
        if (i > k2) {
            if (!queue.isEmpty() && queue.getFirst() < i - k2) {
                   queue.removeFirst();
            }
        }
        if (i >= k1) {
          while (!queue.isEmpty() && sums[queue.getLast()] > sums[i - k1]) {
              queue.removeLast();
          }
          queue.offer(i - k1);
          largestSum = Math.max(largestSum, sums[i] - sums[queue.getFirst()]);
        }
      }
      return largestSum;
    }
}

// Solution 2
class Pair {
     int sum;
     int index;
    public Pair(int sum, int index) {
      this.sum = sum;
      this.index = index;
    }
}

public class Solution {
    /**
     * @param nums an array of integers
     * @param k1 an integer
     * @param k2 an integer
     * @return the largest sum
     */
    public int maxSubarray5(int[] nums, int k1, int k2) {
        // Write your code here
        if (nums == null || nums.length == 0 || nums.length < k1) {
            return 0;
        }
        int largestSum = Integer.MIN_VALUE;
        int[] sums = new int[nums.length + 1];
        sums[0] = 0;
        PriorityQueue<Pair> queue = new PriorityQueue<Pair>(nums.length, new Comparator<Pair>(){
            public int compare(Pair x, Pair y) {
                return x.sum - y.sum;
            }
        });
        for (int i = 1; i <= nums.length; i++) {
              sums[i] = sums[i - 1] + nums[i - 1];
            if (k1 <= i && i <= k2) {
                queue.offer(new Pair(sums[i - k1], i - k1));
                if (!queue.isEmpty()) {
                    largestSum = Math.max(largestSum, sums[i] - queue.peek().sum); 
                } 
            }
            if (i > k2) {
              queue.offer(new Pair(sums[i - k1], i - k1));    
              while (!queue.isEmpty() && queue.peek().index < i - k2) {
                  queue.poll();
              }
              largestSum = Math.max(largestSum, sums[i] - queue.peek().sum); 
            }                
        }
        return largestSum;
    }
}
```



