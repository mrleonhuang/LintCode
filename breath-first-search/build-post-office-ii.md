## 573. Build Post Office II \[LintCode\]

> Given a 2D grid, each cell is either a wall`2`, an house`1`or empty`0`\(the number zero, one, two\), find a place to build a post office so that the sum of the distance from the post office to all the houses is smallest.
>
> Return the smallest sum of distance. Return`-1`if it is not possible.
>
> ##### Notice
>
> * You cannot pass through wall and house, but can pass through empty.
> * You only build post office on an empty.
>
> **Example**
>
> Given a grid:
>
> ```
> 0 1 0 0 0
> 1 0 0 2 1
> 0 1 0 0 0
> ```
>
> return `8`, You can build at`(1,1)`. \(Placing a post office at \(1,1\), the distance that post office to all the house sum is smallest.\)

distanceSum和visitedTimes数组记录每一个empty节点的信息。

BFS是从每一个house出发，去搜索empty节点并且记录。

```java
class Coordinate{
    int x, y;
    public Coordinate(int x, int y){
        this.x = x;
        this.y = y;
    }
}

public class Solution {
    /**
     * @param grid a 2D grid
     * @return an integer
     */
    public static final int EMPTY = 0;
    public static final int HOUSE = 1;
    public static final int WALL = 2;
    public int[][] grid;
    public int m;
    public int n;
    public int[] dirX = {0, 0, 1, -1};
    public int[] dirY = {1, -1, 0, 0};

    public int shortestDistance(int[][] grid) {
        if(grid == null || grid.length == 0 || grid[0].length == 0)
            return -1;

        setGrid(grid);

        int[][] distanceSum = new int[m][n];
        int[][] visitedTimes = new int[m][n];

        ArrayList<Coordinate> houses = getCoordinates(HOUSE);
        for (Coordinate house : houses) {
            bfs(house, distanceSum, visitedTimes);
        }

        int shortest = Integer.MAX_VALUE;
        ArrayList<Coordinate> empties = getCoordinates(EMPTY);
        for (Coordinate empty : empties) {
            if(visitedTimes[empty.x][empty.y] != houses.size())
                continue;
            shortest = Math.min(shortest, distanceSum[empty.x][empty.y]);
        }

        if(shortest == Integer.MAX_VALUE) 
            return -1;

        return shortest;
    }

    private void setGrid(int[][] grid){
        this.m = grid.length;
        this.n = grid[0].length;
        this.grid = grid;
    }

    private ArrayList<Coordinate> getCoordinates(int type){
        ArrayList<Coordinate> coordinates = new ArrayList();
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(grid[i][j] == type){
                    coordinates.add(new Coordinate(i, j));
                }
            }
        }
        return coordinates;
    }

    private void bfs(Coordinate start, int[][] distanceSum, int[][] visitedTimes) {

        boolean[][] visited = new boolean[m][n];
        Queue<Coordinate> queue = new LinkedList<Coordinate>();
        int step = 0;
        queue.offer(start);
        visited[start.x][start.y] = true;
        while(!queue.isEmpty()){
            step++;
            int size = queue.size();
            for(int i = 0; i < size; i++){
                Coordinate head = queue.poll();
                for(int j = 0; j < 4; j++){
                    Coordinate adj = new Coordinate(head.x + dirX[j], head.y + dirY[j]);
                    if(!isEmptyPoint(adj)) continue;
                    if(visited[adj.x][adj.y]) continue;
                    queue.offer(adj);
                    visited[adj.x][adj.y] = true;
                    distanceSum[adj.x][adj.y] += step;
                    visitedTimes[adj.x][adj.y]++;
                }
            }
        }
    }

    private boolean isEmptyPoint(Coordinate cor){
        if(cor.x < 0 || cor.x >= m) return false;
        if(cor.y < 0 || cor.y >= n) return false;
        return this.grid[cor.x][cor.y] == EMPTY;
    }
}
```



