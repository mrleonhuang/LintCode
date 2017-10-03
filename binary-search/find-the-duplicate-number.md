## 287. Find the Duplicate Number

> Given an array nums containing n + 1 integers where each integer is between 1 and n \(inclusive\), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.
>
> You **must not **modify the array \(assume the array is read only\).  
> You must use only constant,O\(1\) extra space.  
> Your runtime complexity should be less than`O(n2)`  
> There is only one duplicate number in the array, but it could be repeated more than once

n + 1个位置，大小范围是1 - n，只能有一个duplicate的这些条件限定了只有1,2,2,3,4,5这种单一情况。所以用抽屉原理即可。

```java
class Solution {
    public int findDuplicate(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int start = 1;
        int end = nums.length - 1;
        int mid;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (countNum(nums, mid) <= mid) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (countNum(nums, start) > start) {
            return start;
        }
        return end;
    }

    private int countNum(int[] nums, int target) {
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] <= target) {
                count++;
            }
        }
        return count;
    }
}
```



