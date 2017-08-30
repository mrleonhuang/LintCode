# 625. Partition Array II

> Partition an unsorted integer array into three parts:
>
> 1. The front part &lt; low
> 2. The middle part &gt;= low & &lt;= high
> 3. The tail part &gt; high
>
> Return any of the possible solutions.

**刚开始想了一个复杂的4根指针的recursion方法，但是栈溢出。**

**答案：用3-way-partition，有三根指针，把整个数组分为4段**

1. **Left指针代表着指针左边的数都已经check过，是小于范围的**

2. **Right指针代表右边的数已经check过，是大于范围的**

3. **Left指针到中间指针区间是已经check过，是在范围内的数**

4. **中间指针到right指针区间表示还没有被check的数**

**分三种情况：**

1. **如果i的数小于范围，则与左指针交换，left++, i++**

2. **如果i的数大于范围，则与右指针交换，，right--，i不变；**

3. **如果是范围内的数，则 i++（所以和left指针拉出来的空间就是范围内的数）**

```java
public class Solution {
    /**
     * @param nums an integer array
     * @param low an integer
     * @param high an integer
     * @return nothing
     */
    public void partition2(int[] nums, int low, int high) {
        // Write your code here
        if (nums == null || nums.length < 2) {
            return;
        }
        int left = 0;
        int right = nums.length - 1;
        int i = 0;
        while (i <= right) {
            if (nums[i] < low) {
                swap(nums, left++, i++);
            } else if (nums[i] > high) {
                swap(nums, i, right--);
            } else {
                i++;
            }
        }
    }
    
    private void swap(int[] nums, int x, int y) {
        int temp = nums[x];
        nums[x] = nums[y];
        nums[y] = temp;
    }
}
```



