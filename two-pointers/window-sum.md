# 604. Window Sum

> Given an array of n integer, and a moving window\(size k\), move the window at each iteration from the start of the array, find the `sum `of the element inside the window at each moving.
>
> **Example**
>
> For array`[1,2,7,8,5]`, moving window size k =`3`.  
> 1 + 2 + 7 = 10  
> 2 + 7 + 8 = 17  
> 7 + 8 + 5 = 20  
> return`[10,17,20]`

```java
public class Solution {
    /**
     * @param nums a list of integers.
     * @return the sum of the element inside the window at each moving.
     */
    public int[] winSum(int[] nums, int k) {
        // write your code here
        if (nums == null || nums.length == 0 || nums.length < k) {
            return new int[0];
        }
        int[] sums = new int[nums.length - k + 1];
        for (int i = 0; i < nums.length - k + 1; i++) {
            int sum = 0;
            for (int j = i; j < i + k; j++) {
                sum += nums[j];
            }
            sums[i] = sum;
        }
        return sums;
    }
}
```



