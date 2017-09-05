# 160. Find Minimum in Rotated Sorted Array II

> Suppose a sorted array is rotated at some pivot unknown to you beforehand.
>
> \(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2\).
>
> Find the minimum element.
>
> ##### Notice
>
> The array may contain duplicates.
>
> **Example**
>
> Given`[4,4,5,6,7,0,1,2]`return`0`.

如果mid值等于最后一个值，无法判断是0, 1, 2, 2, 2 还是 2, 2, 2, 0, 1, 2， 因此要移动right指针一步，把重复元素都堆到数列左边或者右边，才能破局。

```java
public class Solution {
    /**
     * @param num: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] num) {
        // write your code here
        if (num == null || num.length == 0) {
            return -1;
        }
        int left = 0;
        int right = num.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (num[mid] > num[right]) {
                left = mid;
            } else if (num[mid] < num[right]) {
                right = mid;
            } else {
                right--;
            }
        }
        if (num[left] <= num[right]) {
            return num[left];
        }
        return num[right];
    }
}
```



