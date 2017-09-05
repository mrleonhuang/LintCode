# 28. Search a 2D Matrix

> Write an efficient algorithm that searches for a value in an_m_x_n_matrix.
>
> This matrix has the following properties:
>
> * Integers in each row are sorted from left to right.
> * The first integer of each row is greater than the last integer of the previous row.
>
> **Example**
>
> Consider the following matrix:
>
> ```
> [
>     [1, 3, 5, 7],
>     [10, 11, 16, 20],
>     [23, 30, 34, 50]
> ]
>
> ```
>
> Given`target = 3`, return`true`.

matrix和grid的长宽是固定的矩阵，所以可以用每个坐标序列对于m的除数和余数来得到坐标x, y

```java
public class Solution {
    /*
     * @param matrix: matrix, a list of lists of integers
     * @param target: An integer
     * @return: a boolean, indicate whether matrix contains target
     */
    public boolean searchMatrix(int[][] matrix, int target) {
        // write your code here
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }
        int n = matrix.length;
        int m = matrix[0].length;
        int start = 0;
        int end = n * m - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            int x = mid / m;
            int y = mid % m;
            if (matrix[x][y] <= target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (matrix[start / m][start % m] == target) {
            return true;
        }
        if (matrix[end / m][end % m] == target) {
            return true;
        }
        return false;
    }
}
```



