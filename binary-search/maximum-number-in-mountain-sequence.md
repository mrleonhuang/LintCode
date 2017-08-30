# 585. Maximum Number in Mountain Sequence

> Given a mountain sequence of `n `integers which increase firstly and then decrease, find the mountain top.
>
> **Example**
>
> Given`nums`=`[1, 2, 4, 8, 6, 3]`return`8`  
> Given`nums`=`[10, 9, 8, 7]`, return`10`

```java
public class Solution {
    /**
     * @param nums a mountain sequence which increase firstly and then decrease
     * @return then mountain top
     */
    public int mountainSequence(int[] nums) {
        // Write your code here
        if(nums == null || nums.length == 0) return -1;
        if(nums.length == 1) return nums[0];
        
        int start = 0;
        int end = nums.length - 1;
        int mid;
        
        while(start + 1 < end)
        {
            mid = start + (end - start) / 2;
            
            if(nums[mid] < nums[mid + 1])
            {
                start = mid;
            }
            else
            {
                end = mid;
            }
        }
        
        if(nums[start] >= nums[end]) return nums[start];
        return nums[end];
    }
}
```



