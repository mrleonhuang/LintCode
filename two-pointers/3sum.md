# 15. 3Sum \[LeetCode\]

> Given an array S of n integers, are there elements a, b, c in S such that a+b+c= 0? Find all unique triplets in the array which gives the sum of zero.
>
> **Note:**The solution set must not contain duplicate triplets.
>
> ```
> For example, given array S = [-1, 0, 1, 2, -1, -4],
>
> A solution set is:
> [
>   [-1, 0, 1],
>   [-1, -1, 2]
> ]
> ```

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        if (nums == null || nums.length < 3) {
            return results;
        }
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            if (i != 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int start = i + 1;
            int end = nums.length - 1;
            int sum;
            while (start < end) {
                if (start != i + 1 && nums[start] == nums[start - 1]) {
                    start++;
                    continue;
                }
                if (end != nums.length - 1 && nums[end] == nums[end + 1]) {
                    end--;
                    continue;
                }
                sum = nums[i] + nums[start] + nums[end];
                if (sum < 0) {
                    start++;
                } else if (sum > 0) {
                    end--;
                } else {
                    List<Integer> triplet = new ArrayList<Integer>();
                    triplet.add(nums[i]);
                    triplet.add(nums[start]);
                    triplet.add(nums[end]);
                    results.add(triplet);
                    start++;
                    end--;
                }
            }
        }
        return results;
    }
}
```



