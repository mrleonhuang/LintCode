# 75. Find Peak Element

> There is an integer array which has the following features:
>
> * The numbers in adjacent positions are different.
> * A\[0\] &lt; A\[1\] && A\[A.length - 2\] &gt; A\[A.length - 1\].
>
> We define a position P is a peek if:
>
> ```
> A[P] > A[P-1] && A[P] > A[P+1]
> ```
>
> Find a peak element in this array. Return the index of the peak.
>
> ##### Notice
>
> The array may contains multiple peeks, find any of them.
>
> **Example**
>
> Given`[1, 2, 1, 3, 4, 5, 7, 6]`
>
> Return index`1`\(which is number 2\) or`6`\(which is number 7\)

```java
class Solution {
    /**
     * @param A: An integers array.
     * @return: return any of peek positions.
     */
    public int findPeak(int[] A) {
        // write your code here
        if (A == null || A.length == 0) {
            return -1;
        }
        int left = 1;
        int right = A.length - 2;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (A[mid] < A[mid + 1]) {
                left = mid;
            } else {
                right = mid;
            }
        }
        if (A[left] < A[right]) {
            return right;
        }
        return left;
    }
}
```



