## 378. Kth Smallest Element in a Sorted Matrix \[LeetCode\]

> Given anxnmatrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.
>
> Note that it is the kth smallest element in the sorted order, not the kth distinct element.
>
> **Example:**
>
> ```
> matrix = [
>    [ 1,  5,  9],
>    [10, 11, 13],
>    [12, 13, 15]
> ],
> k = 8,
>
> return 13.
> ```
>
> **Note:**  
> You may assume k is always valid, 1 ≤ k ≤ n2.

1. Heap + BFS：找第k个数首先想到用Heap，图想到BFS，PriorityQueue刚好满足这两个条件。注意用boolean数组去重。
2. 二分搜索：二分搜索中左右坐标的移动不好判断，但是得到启发：

3. 可以用二分搜索找mid的方式来找第k个数

4. check函数提供了这种特定overlap matrix中判断某个数排名的方法（走对角线并统计），中心思想是一个数左上角的所有数肯定都比它小，但是它的右上角也有可能有数字比它小。类似题有Search in 2D Matrix II

```java
// solution 1
class Coordinate {
    int x;
    int y;
    int value;
    public Coordinate(int x, int y, int value) {
        this.x = x;
        this.y = y;
        this.value = value;
    }
}
public class Solution {
    private int n;
    private int m;
    private int[] dirX = {0, 1};
    private int[] dirY = {1, 0};

    public int kthSmallest(int[][] matrix, int k) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return -1;
        }
        this.n = matrix.length;
        this.m = matrix[0].length;
        boolean[][] visited = new boolean[this.n][this.m];
        PriorityQueue<Coordinate> heap = new PriorityQueue<Coordinate>(k + 1, new Comparator<Coordinate>(){
            public int compare(Coordinate x, Coordinate y) {
                return x.value - y.value;
            }
        });
        heap.offer(new Coordinate(0, 0, matrix[0][0]));
        visited[0][0] = true;
        for (int i = 0; i < k - 1; i++) {
            if (heap.isEmpty()) {
                return -1;
            }
            Coordinate min = heap.poll();
            for (int j = 0; j < 2; j++) {
                int next_x = min.x + dirX[j];
                int next_y = min.y + dirY[j];
                if (inBound(next_x, next_y) && !visited[next_x][next_y]) {
                    Coordinate next = new Coordinate(next_x, next_y, matrix[next_x][next_y]);
                    heap.offer(next);
                    visited[next_x][next_y] = true;
                }
            }
        }
        if (heap.isEmpty()) {
            return -1;
        }
        return heap.poll().value;
    }

    private boolean inBound(int x, int y) {
        return x >= 0 && x < this.n && y >= 0 && y < this.m;
    }
}

// solution 2
class ResultType {
    boolean exist;
    int num;
    public ResultType (boolean exist, int num) {
        this.exist = exist;
        this.num = num;
    }
}

public class Solution {
    private int n;
    private int m;
    public int kthSmallest(int[][] matrix, int k) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return -1;
        }
        this.n = matrix.length;
        this.m = matrix[0].length;
        int start = matrix[0][0];
        int end = matrix[n - 1][m - 1];
        int mid;
        while (start <= end) {
            mid = start + (end - start) / 2;
            ResultType type = check(mid, matrix);
            if (type.exist && type.num == k) {
                return mid;
            } else if (type.num < k) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return start;
    }

    private ResultType check(int value, int[][] matrix) {
        int num = 0;
        boolean exist = false;
        int i = this.n - 1;
        int j = 0;
        while (i >= 0 && j < this.m) {
            if (matrix[i][j] == value) {
                exist = true;
            }
            if (matrix[i][j] <= value) {
                num += i + 1;
                j++;
            } else {
                i--;
            }
        }
        return new ResultType(exist, num);
    }
}
```



