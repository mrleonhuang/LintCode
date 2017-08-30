# 458. Last Position of Target

> Find the last position of a target number in a sorted array. Return -1 if target does not exist.
>
> **Example**
>
> Given`[1, 2, 2, 4, 5, 5]`.
>
> For target =`2`, return 2.
>
> For target =`5`, return 5.
>
> For target =`6`, return -1.

```java
public class Solution {
    /**
     * @param nums: An integer array sorted in ascending order
     * @param target: An integer
     * @return an integer
     */
    public int lastPosition(int[] nums, int target) {
        // Write your code here
        
        if(nums == null || nums.length == 0) return -1;
        
        int start = 0;
        int end = nums.length - 1;
        int mid;
        
        while(start + 1 < end)
        {
            mid = start + (end - start) / 2;
            
            if(nums[mid] <= target)
            {
                start = mid;
            }
            else
            {
                end = mid;
            }
        }
        
        if(nums[end] == target) return end;
        else if(nums[start] == target) return start;
        return -1;
    }
}
```



