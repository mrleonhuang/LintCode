## 544. Top k Largest Numbers \[LintCode\]

> Given an integer array, find the top k largest numbers in it.
>
> **Example**
>
> Given`[3,10,1000,-99,4,100]`and _k_=`3`.  
> Return`[1000, 100, 10]`.

1.Min Heap 最小堆： PriorityQueue，把数组里的数加入queue里，保持queue里有k个元素，最后剩下的数就是最大的k个数

* 注意点1：PriorityQueue&lt;Integer&gt;默认是升序，如果需要降序，可以用

  ```java
  PriorityQueue<Integer>queue=newPriorityQueue<Integer>(size,Collections.reverseOrder());
  ```

  或者自定义Comparator

```java
    PriorityQueue<Integer> queue = new PriorityQueue<Integer>(size,new Comparator<Integer>(){
        public int compare(Integer o1, Integer o2){
            if (o1 > o2) return 1;
            if (o1 < o2) return -1;
            if (o1 == o2) return 0;
        }
    }
```

* 注意点2：当queue里有k+1个数的时候poll最小的数出来，这样才是最大的k个数。并且注意poll和插入数的前后顺序。

* 注意点3：输出顺序如果需要从大到小，则需要逆着放进最终结果数组里



2.Max Heap最大堆：PriorityQueue装进所有元素，导出最大的k个

3.Quick Sort 把最大的k个数quickSort到最前面，后面的数顺序不用管，递归出口为start &gt;= k

```java
// solution 1
class Solution {
    /*
     * @param nums an integer array
     * @param k an integer
     * @return the top k largest numbers in array
     */
    public int[] topk(int[] nums, int k) {
        // Write your code here
        if (nums == null || nums.length < k) {
            return new int[0];
        }
        PriorityQueue<Integer> queue = new PriorityQueue<Integer>();
        for (int i = 0; i < nums.length; i++) {
            queue.offer(nums[i]);
            if (queue.size() == k + 1) {
                queue.poll();
            }
        }
        int[] results = new int[k];
        int index = k - 1;
        while (!queue.isEmpty()) {
            results[index--] = queue.poll();
        }
        return results;
    }
};

// solution 2
class Solution {
    /*
     * @param nums an integer array
     * @param k an integer
     * @return the top k largest numbers in array
     */
    public int[] topk(int[] nums, int k) {
        // Write your code here
        if (nums == null || nums.length < k) {
            return new int[0];
        }
        PriorityQueue<Integer> queue = new PriorityQueue<Integer>(nums.length, Collections.reverseOrder());
        for (int i = 0; i < nums.length; i++) {
            queue.offer(nums[i]);
        }
        int[] results = new int[k];
        for (int i = 0; i < k; i++) {
            results[i] = queue.poll();
        }
        return results;
    }
};

// solution 3: 
class Solution {
    /*
     * @param nums an integer array
     * @param k an integer
     * @return the top k largest numbers in array
     */
    public int[] topk(int[] nums, int k) {
        // Write your code here
        if (nums == null || nums.length < k) {
            return new int[k];
        }
        quickSort(nums, 0, nums.length - 1, k);
        int[] results = new int[k];
        for(int i = 0; i < k; i++) {
            results[i] = nums[i];
        }
        return results;
    }

    private void quickSort(int[] nums, int start, int end, int k) {
        if (start >= k || start >= end) {
            return;
        }
        int left = start;
        int right = end;
        int pivot = nums[start + (end - start) / 2];
        while (left <= right) {
            while (left <= right && nums[left] > pivot) {
                left++;
            }
            while (left <= right && nums[right] < pivot) {
                right--;
            }
            if (left <= right) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
                right--;
            }
        }
        quickSort(nums, start, right, k);
        quickSort(nums, left, end, k);
    }
};
```



