# 587. Two Sum - Unique pairs \[LintCode\]

> Given an array of integers, find how many
>
> `unique pairs`
>
> in the array such that their sum is equal to a specific target number. Please return the number of pairs.
>
> **Example**
>
> Given nums =`[1,1,2,45,46,46]`, target =`47`  
> return`2`
>
> 1 + 46 = 47  
> 2 + 45 = 47

1. O\(nlogn\)时间：先排序，然后按照sorted array做。注意左右指针判断nums\[left\] == nums\[left - 1\] 和 nums\[right\] == nums\[right + 1\]
2. O\(n\)时间 + O\(n\)空间：用HashMap记录每个元素出现的次数。遍历哈希表的keySet\(\)，

   如果target - key存在并且和key本身不相等，则记录，并且将当前key和target - key的出现次数都记录为0

   如果target - key存在并且和key本身相等（注意这种特殊情况），则判断本身出现次数是否大于等于2次，如果是，则记录并且重置为0

```java
// Solution 1
public class Solution {
    /**
     * @param nums an array of integer
     * @param target an integer
     * @return an integer
     */
    public int twoSum6(int[] nums, int target) {
        // Write your code here
        if (nums == null || nums.length < 2) {
            return 0;
        }
        Arrays.sort(nums);
        int count = 0;
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            if (left != 0 && nums[left] == nums[left - 1]) {
                left++;
                continue;
            }
            if (right != nums.length - 1 && nums[right] == nums[right + 1]) {
                right--;
                continue;
            }
            if (nums[left] + nums[right] < target) {
                left++;
            } else if (nums[left] + nums[right] > target) {
                right--;
            } else {
                count++;
                left++;
                right--;
            }
        }
        return count;
    }
}

// Solution 2
public class Solution {
    /**
     * @param nums an array of integer
     * @param target an integer
     * @return an integer
     */
    public int twoSum6(int[] nums, int target) {
        // Write your code here
        if (nums == null || nums.length < 2) {
            return 0;
        }
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(nums[i])) {
                map.put(nums[i], map.get(nums[i]) + 1);
            } else {
                map.put(nums[i], 1);
            }
        }
        int count = 0;
        for (int number : map.keySet()) {
            if (map.get(number) == 0) {
                continue;
            }
            int required = target - number;
            if (map.containsKey(required)) {
                if (required == number && map.get(number) > 1) {
                    count++;
                    map.put(number, 0);
                } else if (required != number && map.get(required) > 0) {
                    count++;
                    map.put(number, 0);
                    map.put(required, 0);
                }
            }
        }
        return count;
    }
}
```



