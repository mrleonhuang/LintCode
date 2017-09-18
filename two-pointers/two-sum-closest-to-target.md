# 533. Two Sum - Closest to target \[LintCode\]

> Given an array`nums`of_n\_integers, find two integers in\_nums\_such that the sum is closest to a given number,\_target_.
>
> Return the difference between the sum of the two integers and the target.
>
> **Example**
>
> Given array`nums`=`[-1, 2, 1, -4]`, and_target_=`4`.
>
> The minimum difference is`1`. \(4 - \(2 + 1\) = 1\).

```java
public class Solution {
    /**
     * @param nums an integer array
     * @param target an integer
     * @return the difference between the sum and the target
     */
    public int twoSumClosest(int[] nums, int target) {
        // Write your code here
        int minDiff = Integer.MAX_VALUE;
        if (nums == null || nums.length == 0 || nums.length == 1) {
            return minDiff;
        }
        Arrays.sort(nums);
        int start = 0;
        int end = nums.length - 1;
        while (start < end) {
            int sum = nums[start] + nums[end];
            minDiff = Math.min(minDiff, Math.abs(target - sum));
            if (sum < target) {
                start++;
            } else if (sum > target) {
                end--;
            } else {
                break;
            }
        }
        return minDiff;
    }
}

//  结合二分搜索，炫技了。
public class Solution {
    /**
     * @param nums an integer array
     * @param target an integer
     * @return the difference between the sum and the target
     */
    public int twoSumClosest(int[] nums, int target) {
        // Write your code here
        int minDiff = Integer.MAX_VALUE;
        if (nums == null || nums.length == 0 || nums.length == 1) {
            return minDiff;
        }
        Arrays.sort(nums);
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end) {
            int sum = nums[start] + nums[end];
            if (sum == target) {
                return 0;
            }
            minDiff = Math.min(minDiff, Math.abs(target - sum));
            int mid = start + (end - start) / 2;
            if (sum < target) {
                if (nums[mid] + nums[end] <= target) {
                    start = mid;
                } else {
                    start++;
                }
            } else if (sum > target) {
                if (nums[start] + nums[mid] >= target) {
                    end = mid;
                } else {
                    end--;
                }
            } 
        }
        minDiff = Math.min(minDiff, Math.abs(target - nums[start] - nums[end]));
        return minDiff;
    }
}
```



