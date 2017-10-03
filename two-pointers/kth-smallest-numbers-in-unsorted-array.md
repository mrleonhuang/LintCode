## 461. Kth Smallest Numbers in Unsorted Array \[LintCode\]

> Find the kth smallest numbers in an unsorted integer array.
>
> **Example**
>
> Given`[3, 4, 1, 2, 5]`, k =`3`, the 3rd smallest numbers are`[1, 2, 3]`.

**Kth Smallest Numbers in Unsorted Array &**

**Kth Largest Element &**

**Median**

用一个叫做Quick Select的方法，是快速排序的步骤。

每执行一次，可以将比pivot大（小）的数归到数组的左侧，比pivot小（大）的数都归到数组右侧，并得到这个pivot的坐标。这样得到两段（或者三段），第一段是start ~ right，第二段是left ~ end，有可能中间有一个元素right + 1（left - 1\)。比较k在哪个区间，则继续递归那个区间。

时间复杂度为O\(n\) ： 用O\(n\)的方法将T\(n\)的问题变成T\(n/2\)的问题。

```java
class Solution {
    /*
     * @param k an integer
     * @param nums an integer array
     * @return kth smallest element
     */
    public int kthSmallest(int k, int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return -1;
        }
        return quickSelect(nums, 0, nums.length - 1, k - 1);
    }

    private int quickSelect(int[] nums, int start, int end, int k) {
        int left = start;
        int right = end;
        int pivot = nums[start + (end - start) / 2];
        while (left <= right) {
            while (left <= right && nums[left] < pivot) {
                left++;
            }
            while (left <= right && nums[right] > pivot) {
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
        if (start <= k && k <= right) {
            return quickSelect(nums, start, right, k);
        }
        if (left <= k && k <= end) {
            return quickSelect(nums, left, end, k);
        }
        return nums[right + 1];
    }
};
```



