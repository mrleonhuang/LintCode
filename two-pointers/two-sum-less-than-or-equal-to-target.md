# 609. Two Sum - Less than or equal to target

> Given an array of integers, find how many pairs in the array such that their sum is
>
> `less than or equal to`a specific target number. Please return the number of pairs.
>
> **Example**
>
> Given nums =`[2, 7, 11, 15]`, target =`24`.  
> Return`5`.  
> 2 + 7 &lt; 24  
> 2 + 11 &lt; 24  
> 2 + 15 &lt; 24  
> 7 + 11 &lt; 24  
> 7 + 15 &lt; 25

**先排序：**

**如果当前nums\[left\] + nums\[right\] &lt;= target, 说明在当前left的位置，加上right指针这么大的数都是符合条件的，那么加上right指针所有左边的数肯定都是符合条件的。因此count += right - left.**

```java
public class Solution {
    /**
     * @param nums an array of integer
     * @param target an integer
     * @return an integer
     */
    public int twoSum5(int[] nums, int target) {
        // Write your code here
        if (nums == null || nums.length < 2) {
            return 0;
        }
        Arrays.sort(nums);
        int count = 0;
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            if (nums[left] + nums[right] > target) {
                right--;
            } else {
                count += right - left;
                left++;
            }
        }
        return count;
    }
}
```

  




