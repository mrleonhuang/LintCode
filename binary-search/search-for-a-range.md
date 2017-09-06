# 61. Search for a Range

> Given a sorted array of_n_integers, find the starting and ending position of a given target value.
>
> If the target is not found in the array, return`[-1, -1]`.
>
> **Example**
>
> Given`[5, 7, 7, 8, 8, 10]`and target value`8`,  
> return`[3, 4]`.

分两次搜索前后bound，类似于Total Occurrence of Target

```java
public class Solution {
    /*
     * @param A: an integer sorted array
     * @param target: an integer to be inserted
     * @return: a list of length 2, [index1, index2]
     */
    public int[] searchRange(int[] A, int target) {
        // write your code here
        int[] result = new int[2];
        result[0] = result[1] = -1;
        if (A == null || A.length == 0) {
            return result;
        }
        int start = 0;
        int end = A.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (A[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (A[start] == target) {
            result[0] = start;
        } else if (A[end] == target) {
            result[0] = end;
        } else {
            return result;
        }
        start = 0;
        end = A.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (A[mid] <= target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (A[end] == target) {
            result[1] = end;
        } else if (A[start] == target) {
            result[1] = start;
        } else {
            return result;
        }
        return result;
    }
}
```



