## 620. Maximum Subarray IV \[LintCode\]

> Given an integer arrays, find a contiguous subarray which has the largest sum and length should be greater or equal to given length`k`.  
> Return the largest sum, return 0 if there are fewer than k elements in the array.
>
> ##### Notice
>
> Ensure that the result is an integer type
>
> **Example**
>
> Given the array`[-2,2,-3,4,-1,2,1,-5,3]`and k =`5`, the contiguous subarray`[2,-3,4,-1,2,1]`has the largest sum =`5`.

思想和Maximum Subarray类似，只不过长度要求k以上。因此和第一题不同的点在于:第一题计算prefixSum的时候，每次循环到一个节点，算minPrefix的时候，相当于从第1个数就开始找，一直到当前节点的前一个数（i - 1）为止，找最小的prefix sum；而这道题从第k个数开始才开始用minPrefix （因为之前不满足k的条件），然后循环到每个节点的时候，相当于从第1个数开始找，一直找到当前数的之前的k个数为止（i - k），找最小的prefix sum。

```java
public class Solution {
    /**
     * @param nums an array of integers
     * @param k an integer
     * @return the largest sum
     */
    public int maxSubarray4(int[] nums, int k) {
        // Write your code here
        if (nums == null || nums.length == 0 || nums.length < k) {
            return 0;
        }
        int largestSum = 0;
        for (int i = 0; i < k; i++) {
            largestSum += nums[i];
        }
        int[] prefixSums = new int[nums.length + 1];
        prefixSums[0] = 0;
        int minPrefix = prefixSums[0];
        for (int i = 1; i <= nums.length; i++) {
            prefixSums[i] = prefixSums[i - 1] + nums[i - 1];
            if (i > k) {
                minPrefix = Math.min(minPrefix, prefixSums[i - k]);
                  largestSum = Math.max(largestSum, prefixSums[i] - minPrefix);
            }
        }
        return largestSum;
    }
}
```



