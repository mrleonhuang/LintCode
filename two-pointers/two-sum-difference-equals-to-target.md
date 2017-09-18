# 610. Two Sum - Difference equals to target \[LintCode\]

> Given an array of integers, find two numbers that their
>
> `difference`
>
> equals to a target value. where index1 must be less than index2. Please note that your returned answers \(both index1 and index2\) are NOT zero-based.

比普通Two Sum多考虑一种情况，同时考虑nums\[i\] + target 和 nums\[i\] - target是否已经存在。

```java
public class Solution {
    /*
     * @param nums an array of Integer
     * @param target an integer
     * @return [index1 + 1, index2 + 1] (index1 < index2)
     */
    public int[] twoSum7(int[] nums, int target) {
        // write your code here
        int[] indices = new int[2];
        if (nums == null || nums.length == 0 || nums.length == 1) {
            return indices;
        }
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(nums[i] + target)) {
                indices[0] = map.get(nums[i] + target) + 1;
                indices[1] = i + 1;
                return indices;
            }
            if (map.containsKey(nums[i] - target)) {
                indices[0] = map.get(nums[i] - target) + 1;
                indices[1] = i + 1;
                return indices;
            }
            map.put(nums[i], i);
        }
        return indices;
    }
}
```



