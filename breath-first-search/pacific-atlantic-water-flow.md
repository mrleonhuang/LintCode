## 417. Pacific Atlantic Water Flow

> Given an`m x n`matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.
>
> Water can only flow in four directions \(up, down, left, or right\) from a cell to another one with height equal or lower.
>
> Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.
>
> **Note:**
>
> 1. The order of returned grid coordinates does not matter.
> 2. Both m and n are less than 150.
>
> **Example:**
>
> ```
> Given the following 5x5 matrix:
>
>   Pacific ~   ~   ~   ~   ~ 
>        ~  1   2   2   3  (5) *
>        ~  3   2   3  (4) (4) *
>        ~  2   4  (5)  3   1  *
>        ~ (6) (7)  1   4   5  *
>        ~ (5)  1   1   2   4  *
>           *   *   *   *   * Atlantic
>
> Return:
>
> [[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
> ```

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
    public List<int[]> pacificAtlantic(int[][] matrix) {
        List<int[]> results = new ArrayList<>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return results;
        }
        this.n = matrix.length;
        this.m = matrix[0].length;
        boolean[][] pGrid = new boolean[this.n][this.m];
        boolean[][] aGrid = new boolean[this.n][this.m];
        for (int i = 0; i < this.m; i++) {
            Coordinate pStart = new Coordinate(0, i);
            markByBFS(matrix, pStart, pGrid); 
            Coordinate aStart = new Coordinate(this.n - 1, i);
            markByBFS(matrix, aStart, aGrid);
        }
        for (int i = 0; i < this.n; i++) {
            Coordinate pStart = new Coordinate(i, 0);
            markByBFS(matrix, pStart, pGrid);
            Coordinate aStart = new Coordinate(i, this.m - 1);
            markByBFS(matrix, aStart, aGrid);
        }
        for (int i = 0; i < this.n; i++) {
            for (int j = 0; j < this.m; j++) {
                if (pGrid[i][j] && aGrid[i][j]) {
                    int[] point = new int[2];
                    point[0] = i;
                    point[1] = j;
                    results.add(point);
                }
            }
        }
        return results;
    }
    
    // BFS solution
    private void markByBFS(int[][] matrix, Coordinate start, boolean[][] grid) {
        boolean[][] visited = new boolean[this.n][this.m];
        Queue<Coordinate> queue = new LinkedList<Coordinate>();
        queue.offer(start);
        visited[start.x][start.y] = true;
        grid[start.x][start.y] = true;
        while (!queue.isEmpty()) {
            Coordinate head = queue.poll();
            for (int dir = 0; dir < 4; dir++) {
                int neiX = head.x + dirX[dir];
                int neiY = head.y + dirY[dir];
                if (inBound(neiX, neiY) && !visited[neiX][neiY] && matrix[head.x][head.y] <= matrix[neiX][neiY]) {
                    Coordinate nei = new Coordinate(neiX, neiY);
                    queue.offer(nei);
                    visited[neiX][neiY] = true;
                    grid[neiX][neiY] = true;
                }
            }
        }
    }
    
    // DFS solution
    private void markByDFS(int[][] matrix, Coordinate cor, boolean[][] grid) {
        grid[cor.x][cor.y] = true;
        for (int dir = 0; dir < 4; dir++) {
            int neiX = cor.x + dirX[dir];
            int neiY = cor.y + dirY[dir];
            if (inBound(neiX, neiY) && grid[neiX][neiY] == false && matrix[cor.x][cor.y] <= matrix[neiX][neiY]) {
                markByDFS(matrix, new Coordinate(neiX, neiY), grid);
            }
        }
    }

    private boolean inBound(int x, int y) {
        return x >= 0 && x < this.n && y >= 0 && y < this.m;
    }
}
```



