## 542. 01 Matrix

> Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.
>
> The distance between two adjacent cells is 1.
>
> **Example 1:**  
> Input:
>
> ```
> 0 0 0
> 0 1 0
> 0 0 0
> ```
>
> Output:
>
> ```
> 0 0 0
> 0 1 0
> 0 0 0
> ```
>
> **Example 2:**  
> Input:
>
> ```
> 0 0 0
> 0 1 0
> 1 1 1
> ```
>
> Output:
>
> ```
> 0 0 0
> 0 1 0
> 1 2 1
> ```
>
> **Note:**
>
> 1. The number of elements of the given matrix will not exceed 10,000.
> 2. There are at least one 0 in the given matrix.
> 3. The cells are adjacent in only four directions: up, down, left and right.

分时去做BFS会超时，要用同时BFS的办法

```java
class Coordinate {
    int x;
    int y;
    public Coordinate(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

public class Solution {
    private int n;
    private int m;
    private int[] dirX = {0, 0, 1, -1};
    private int[] dirY = {1, -1, 0, 0};
    public int[][] updateMatrix(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return new int[0][0];
        }
        this.n = matrix.length;
        this.m = matrix[0].length;
        List<Coordinate> zeros = new ArrayList<>();
        for (int i = 0; i < this.n; i++) {
            for (int j = 0; j < this.m; j++) {
                if (matrix[i][j] == 0) {
                    Coordinate zero = new Coordinate(i, j);
                    zeros.add(zero);
                } else {
                    matrix[i][j] = Integer.MAX_VALUE;
                }
            }
        }
        Queue<Coordinate> queue = new LinkedList<Coordinate>();
        for (Coordinate zero : zeros) {
            queue.offer(zero);
        }
        while (!queue.isEmpty()) {
            Coordinate head = queue.poll();
            for (int dir = 0; dir < 4; dir++) {
                int neiX = head.x + dirX[dir];
                int neiY = head.y + dirY[dir];
                if (inBound(neiX, neiY) && matrix[neiX][neiY] > matrix[head.x][head.y] + 1) {
                    matrix[neiX][neiY] = matrix[head.x][head.y] + 1;
                    queue.offer(new Coordinate(neiX, neiY));
                }
            }
        }
        return matrix;
    }

    private boolean inBound(int x, int y) {
        return x >= 0 && x < this.n && y >= 0 && y < this.m;
    }
}
```



