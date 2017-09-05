# 462. Total Occurrence of Target

> Given a target number and an integer array sorted in ascending order. Find the total number of occurrences of target in the array.
>
> **Example**
>
> Given`[1, 3, 3, 4, 5]`and target =`3`, return`2`.
>
> Given`[2, 2, 3, 4, 6]`and target =`4`, return`1`.
>
> Given`[1, 2, 3, 4, 5]`and target =`6`, return`0`.

两次查找，分别找左边界和右边界。通过**A\[mid\] == target时候的指针调整**和**最后判断start, end指针是否为target的顺序**，来决定本次查找是尽可能向左还是向右。

```java
public class Solution {
    /*
     * @param A: an integer array sorted in ascending order
     * @param target: An integer
     * @return: An integer
     */
    public int totalOccurrence(int[] A, int target) {
        // write your code here
        if (A == null || A.length == 0) {
            return 0;
        }
        int start = 0; 
        int end = A.length - 1;
        int mid, first, last;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (A[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (A[start] == target) {
            first = start;
        } else if (A[end] == target) {
            first = end;
        } else {
            return 0;
        }
        start = 0; 
        end = A.length - 1;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (A[mid] <= target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (A[end] == target) {
            last = end;
        } else if (A[start] == target) {
            last = start;
        } else {
            return 0;
        }
        return last - first + 1;
    }
}
```



