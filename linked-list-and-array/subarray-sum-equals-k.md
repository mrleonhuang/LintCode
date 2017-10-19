## 560. Subarray Sum Equals K

> Given an array of integers and an integer**k**, you need to find the total number of continuous subarrays whose sum equals to**k**.
>
> **Example 1:**
>
> ```
> Input: nums = [1,1,1], k = 2
> Output:2
> ```
>
> **Note:**
>
> 1. The length of the array is in range \[1, 20,000\].
> 2. The range of numbers in the array is \[-1000, 1000\] and the range of the integer **k **is \[-1e7, 1e7\].

1. 两遍循环O\(n^2\)
2. 用空间复杂度HashMap换时间复杂度

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int number = 0;
        int[] sums = new int[nums.length + 1];
        sums[0] = 0;
        for (int i = 1; i <= nums.length; i++) {
            sums[i] = sums[i - 1] + nums[i - 1];
            for (int j = 0; j < i; j++) {
                if (sums[i] - sums[j] == k) {
                    number++;
                }
            }
        }
        return number;
    }
}
```

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        Map<Integer, Integer> map = new HashMap<>();
        int number = 0;
        int[] sums = new int[nums.length + 1];
        sums[0] = 0;
        map.put(0, 1);
        for (int i = 1; i <= nums.length; i++) {
            sums[i] = sums[i - 1] + nums[i - 1];
            if (map.containsKey(sums[i] - k)) {
                number += map.get(sums[i] - k);
            }
            if (map.containsKey(sums[i])) {
                map.put(sums[i], map.get(sums[i]) + 1);
            } else {
                map.put(sums[i], 1);
            }
        }
        return number;
    }
}
```



