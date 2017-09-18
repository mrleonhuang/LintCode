# 460. K Closest Numbers In Sorted Array \[LintCode\]

> Given a target number, a non-negative integer `k`and an integer array A sorted in ascending order, find the k closest numbers to target in A, sorted in ascending order by the difference between the number and target. Otherwise, sorted in ascending order by number if the difference is same.
>
> **Example**
>
> Given A =`[1, 2, 3]`, target =`2`and k =`3`, return`[2, 1, 3]`.
>
> Given A =`[1, 4, 6, 8]`, target =`3`and k =`3`, return`[4, 1, 6]`.

用二分搜索找到距离target最近的index作为startIndex，然后用two pointers从startIndex开始往前后两个方向进行搜索，类似于merge two sorted arrays的while循环

```java
public class Solution {
    /*
     * @param A: an integer array
     * @param target: An integer
     * @param k: An integer
     * @return: an integer array
     */
    public int[] kClosestNumbers(int[] A, int target, int k) {
        // write your code here
        if (A == null || A.length == 0 || k <= 0 || A.length < k) {
            return new int[0];
        }
        int startIndex = findStartIndex(A, target);
        int[] results = new int[k];
        int index = 0;
        results[index++] = A[startIndex];
        int i = startIndex - 1;
        int j = startIndex + 1;
        while (i >= 0 && j < A.length && index < k) {
            if (Math.abs(A[i] - target) <= Math.abs(A[j] - target)) {
                results[index++] = A[i--];
            } else {
                results[index++] = A[j++];
            }    
        }
        while (i >= 0 && index < k) {
            results[index++] = A[i--];
        }
        while (j < A.length && index < k) {
            results[index++] = A[j++];
        }
        return results;
    }

    private int findStartIndex(int[] A, int target) {
        int left = 0;
        int right = A.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (A[mid] < target) {
                left = mid;
            } else {
                right = mid;
            }
        }
        if (Math.abs(A[left] - target) <= Math.abs(A[right] - target)) {
            return left;
        }
        return right;
    }
}
```



