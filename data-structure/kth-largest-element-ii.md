## 606. Kth Largest Element II \[LintCode\]

> Find K-th largest element in an array. and N is much larger than k.
>
> ##### Notice
>
> You can swap elements in the array
>
> **Example**
>
> In array`[9,3,2,4,8]`, the`3rd`largest element is`4`.
>
> In array`[1,2,3,4,5]`, the`1st`largest element is`5`,`2nd`largest element is`4`,`3rd`largest element is`3`and etc.

```java
class Solution {
    /**
     * @param nums an integer unsorted array
     * @param k an integer from 1 to n
     * @return the kth largest element
     */
    public int kthLargestElement2(int[] nums, int k) {
        // Write your code here
        if (nums == null || nums.length == 0 || nums.length < k) {
            return -1;
        }
        PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>(k + 1);
        for (int number : nums) {
            minHeap.offer(number);
            if (minHeap.size() == k + 1) {
                minHeap.poll();
            }
        }
        return minHeap.peek();
    }
};
```



