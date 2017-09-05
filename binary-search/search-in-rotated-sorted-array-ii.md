# 63. Search in Rotated Sorted Array II

> Follow up for[Search in Rotated Sorted Array](http://www.lintcode.com/problem/search-in-rotated-sorted-array/):
>
> What if**duplicates**are allowed?
>
> Would this affect the run-time complexity? How and why?
>
> Write a function to determine if a given target is in the array.
>
> **Example**
>
> Given`[1, 1, 0, 1, 1, 1]`and target =`0`, return`true`.  
> Given`[1, 1, 1, 1, 1, 1]`and target =`0`, return`false`.

类似于Find Minimum in Rotated Sorted Array II，遇到A\[start\] == A\[mid\]的情况下不知道是2, 2, 2, 0, 1, 2 还是 2, 3, 4, 2, 2, 2的情况，无法判断指针移动情况，因此要指针一格一格移动来将重复元素过滤到单边。

```java
public class Solution {
    /*
     * @param A: an integer ratated sorted array and duplicates are allowed
     * @param target: An integer
     * @return: a boolean 
     */
    public boolean search(int[] A, int target) {
        // write your code here
        if (A == null || A.length == 0) {
            return false;
        }
        int start = 0;
        int end = A.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (A[start] < A[mid]) {
                if (A[start] <= target && target <= A[mid]) {
                    end = mid;
                } else {
                    start = mid;
                }
            } else if (A[start] > A[mid]) {
                if (A[mid] <= target && target <= A[end]) {
                    start = mid;
                } else {
                    end = mid;
                }
            } else {
                start++;
            }
        }
        if (A[start] == target || A[end] == target) {
            return true;
        }
        return false;
    }
}
```



