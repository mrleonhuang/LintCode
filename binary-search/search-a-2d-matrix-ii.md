# 38. Search a 2D Matrix II \[LintCode\]

> Write an efficient algorithm that searches for a value in an m x n matrix, return the occurrence of it.
>
> This matrix has the following properties:
>
> * Integers in each row are sorted from left to right.
> * Integers in each column are sorted from up to bottom.
> * No duplicate integers in each row or column.
>
> **Example**
>
> Consider the following matrix:
>
> ```
> [
>   [1, 3, 5, 7],
>   [2, 4, 7, 8],
>   [3, 5, 9, 10]
> ]
> ```
>
> Given target =`3`, return`2`.

对比第一题，本题每一行有overlap，所以不能拉成一个序列进行二分搜索。但是可以针对每一行或者每一列单独进行二分搜索，复杂度为O\(m\*logn\)或O\(n\*logm\)。

还可以用走对角线的方法，因为在垂直和水平方向分别是递增的，所以当一个元素大于或者小于target的时候，可以排除掉一行或者一列（x++, y--\)，复杂度为O\(m + n\)

```java
public class Solution {
    /**
     * @param matrix: A list of lists of integers
     * @param: A number you want to search in the matrix
     * @return: An integer indicate the occurrence of target in the given matrix
     */
    public int searchMatrix(int[][] matrix, int target) {
        // write your code here
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int count = 0;
        int x = 0;
        int y = matrix[0].length - 1;
        while (x < matrix.length && y >= 0) {
            if (matrix[x][y] < target) {
                x++;
            } else if (matrix[x][y] > target) {
                y--;
            } else {
                count++;
                y--;
                x++;
            }
        }
        return count;
    }
}
```



