## 18. 4Sum \[LeetCode\]

> Given an array S of n integers, are there elements a,b,c, and d in S such that a+b+c+d= target? Find all unique quadruplets in the array which gives the sum of target.
>
> **Note:**The solution set must not contain duplicate quadruplets.
>
> ```
> For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.
> ```
>
> ```
> A solution set is:
> [
>   [-1,  0, 0, 1],
>   [-2, -1, 1, 2],
>   [-2,  0, 0, 2]
> ]
> ```

注意每一层的去重条件为_排除每一层的第一个元素_，不一定是index为0的元素。类似于DFS里的去重。

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> results = new ArrayList<>();
        if (nums == null || nums.length < 4) {
            return results;
        }
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 3; i++) {
            if (i != 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            for (int j = i + 1; j < nums.length - 2; j++) {
                if (j != i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                int start = j + 1;
                int end = nums.length - 1;
                while (start < end) {
                    if (start != j + 1 && nums[start] == nums[start - 1]) {
                        start++;
                        continue;
                    }
                    if (end != nums.length - 1 && nums[end] == nums[end + 1]) {
                        end--;
                        continue;
                    }
                    int sum = nums[i] + nums[j] + nums[start] + nums[end];
                    if (sum < target) {
                        start++;
                    } else if (sum > target) {
                        end--;
                    } else {
                        List<Integer> quad = new ArrayList<Integer>();
                        quad.add(nums[i]);
                        quad.add(nums[j]);
                        quad.add(nums[start]);
                        quad.add(nums[end]);
                        results.add(quad);
                        start++;
                        end--;
                    }
                }
            }
        }
        return results;
    }
}
```



