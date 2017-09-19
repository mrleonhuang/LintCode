# 378. Kth Smallest Element in a Sorted Matrix \[LeetCode\]

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
>
> ```
>
> **Note:**  
> You may assume k is always valid, 1 ≤ k ≤ n2.

```java
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
```



