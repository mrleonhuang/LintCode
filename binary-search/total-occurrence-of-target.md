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

```java
public class Solution {
    /**
     * @param A an integer array sorted in ascending order
     * @param target an integer
     * @return an integer
     */
    public int totalOccurrence(int[] A, int target) {
        // Write your code here
        if(A == null || A.length == 0) return 0;

        // find the left bound (first occurrence position)
        int first; int last;
        int start = 0;
        int end = A.length - 1;
        int mid;

        while(start + 1 < end)
        {
            mid = start + (end - start) / 2;

            if(A[mid] < target)
            {
                start = mid;
            }
            else
            {
                end = mid;
            }
        }

        if(A[start] == target) first = start;
        else if(A[end] == target) first = end;
        else return 0;

        // find the right bound (last occurrence position)
        start = 0;
        end = A.length - 1;

        while(start + 1 < end)
        {
            mid = start + (end - start) / 2;

            if(A[mid] <= target)
            {
                start = mid;
            }
            else
            {
                end = mid;
            }
        }

        if(A[end] == target) last = end;
        else if(A[start] == target) last = start;
        else return 0;

        return last - first + 1;
    }
}
```



