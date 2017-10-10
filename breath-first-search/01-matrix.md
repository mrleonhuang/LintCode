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

分时去做BFS会超时，要用同时BFS的办法，并且对于任何本身已经很小的点，不再加入queue

```java
// BFS
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

DFS要从1的点开始搜索，如果从0开始搜索会超时

```java
class Solution {
    private int n;
    private int m;
    public int[][] updateMatrix(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return new int[0][0];
        }
        this.n = matrix.length;
        this.m = matrix[0].length;
        for (int i = 0; i < this.n; i++) {
            for (int j = 0; j < this.m; j++) {
                if (matrix[i][j] == 0) {
                    continue;
                } else {
                   if (hasZeroNeighbor(matrix, i, j)) {
                       continue;
                   } else {
                       matrix[i][j] = Integer.MAX_VALUE;
                   }
                }
            }
        }
        for (int i = 0; i < this.n; i++) {
            for (int j = 0; j < this.m; j++) {
                if (matrix[i][j] == 1) {
                    dfs(matrix, i, j, -1);
                }
            }
        }
        return matrix;
    }
    
    private void dfs(int[][] matrix, int x, int y, int lastValue) {
        if (!inBound(x, y) || matrix[x][y] < lastValue + 1) {
            return;
        }
        if (lastValue >= 0) matrix[x][y] = lastValue + 1;
        dfs(matrix, x + 1, y, matrix[x][y]);
        dfs(matrix, x - 1, y, matrix[x][y]);
        dfs(matrix, x, y + 1, matrix[x][y]);
        dfs(matrix, x, y - 1, matrix[x][y]);
    }
    
    private boolean hasZeroNeighbor(int[][] matrix, int x, int y) {
        if (x < this.n - 1 && matrix[x + 1][y] == 0) return true;
        if (x > 0 && matrix[x - 1][y] == 0) return true;
        if (y > 0 && matrix[x][y - 1] == 0) return true;
        if (y < this.m - 1 && matrix[x][y + 1] == 0) return true;
        return false;
    }
    
    private boolean inBound(int x, int y) {
        return x >= 0 && x < this.n && y >= 0 && y < this.m;
    }
}
```



