## 167. Two Sum II - Input array is sorted \[LeetCode\]

> Given an array of integers that is already**sorted in ascending order**, find two numbers such that they add up to a specific target number.
>
> The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers \(both index1 and index2\) are not zero-based.
>
> You may assume that each input would haveexactlyone solution and you may not use thesameelement twice.
>
> **Input:**numbers={2, 7, 11, 15}, target=9  
> **Output:**index1=1, index2=2

炫技方法：二分搜索化Two Pointers

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] results = new int[2];
        if (numbers == null || numbers.length < 2) {
            return results;
        }
        int start = 0;
        int end = numbers.length - 1;
        int mid;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (numbers[start] + numbers[end] < target) {
                if (numbers[mid] + numbers[end] <= target) {
                    start = mid;
                } else {
                    start++;
                }
            } else if (numbers[start] + numbers[end] > target) {
                if (numbers[start] + numbers[mid] >= target) {
                    end = mid;
                } else {
                    end--;
                }
            } else {
                results[0] = start + 1;
                results[1] = end + 1;
                return results;
            }
        }
        if (numbers[start] + numbers[end] == target) {
            results[0] = start + 1;
            results[1] = end + 1;
        }
        return results;
    }
}
```



