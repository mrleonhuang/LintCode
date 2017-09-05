# 62. Search in Rotated Sorted Array

> Suppose a sorted array is rotated at some pivot unknown to you beforehand.
>
> \(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).
>
> You are given a target value to search. If found in the array return its index, otherwise return -1.
>
> You may assume no duplicate exists in the array.
>
> **Example**
>
> For`[4, 5, 1, 2, 3]`and`target=1`, return`2`.
>
> For`[4, 5, 1, 2, 3]`and`target=0`, return`-1`.

用A\[start\] 和 A\[mid\]的关系判断哪一段是递增区间，判断出哪一段是递增区间之后，可以判断target是否在递增区间内，从而调整start或者end指针达到减半目的。

```java
public class Solution {
    /*
     * @param A: an integer rotated sorted array
     * @param target: an integer to be searched
     * @return: an integer
     */
    public int search(int[] A, int target) {
        // write your code here
        if (A == null || A.length == 0) {
            return -1;
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
            } else {
                if (A[mid] <= target && target <= A[end]) {
                    start = mid;
                } else {
                    end = mid;
                }
            }
        }
        if (A[start] == target) {
            return start;
        }
        if (A[end] == target) {
            return end;
        }
        return -1;
    }
}
```



