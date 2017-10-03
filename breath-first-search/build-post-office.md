## 574. Build Post Office \[LintCode\]

> Given a 2D grid, each cell is either an house`1`or empty`0`\(the number zero, one\), find the place to build a post office, the distance that post office to all the house sum is smallest. Return the smallest distance. Return`-1`if it is not possible.
>
> ##### Notice
>
> * You can pass through house and empty.
> * You only build post office on an empty.
>
> **Example**
>
> Given a grid:
>
> ```
> 0 1 0 0
> 1 0 1 1
> 0 1 0 0
> ```
>
> return `6`. \(Placing a post office at \(1,1\), the distance that post office to all the house sum is smallest.\)

```java
class Coordinate{
    int x; 
    int y;
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
    public int HOUSE = 1;
    public int EMPTY = 0;
    public int n;
    public int m;
    public int[] dirX = {0, 0, 1, -1};
    public int[] dirY = {1, -1, 0, 0};

    public int shortestDistance(int[][] grid) {
        // Write your code here
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return -1;
        }
        int shortestPath = Integer.MAX_VALUE;
        this.n = grid.length;
        this.m = grid[0].length;
        List<Coordinate> houses = new ArrayList<Coordinate>();
        List<Integer> arrX = new ArrayList<Integer>();
        List<Integer> arrY = new ArrayList<Integer>();
        boolean[][] visited = new boolean[this.n][this.m];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (grid[i][j] == HOUSE) {
                    houses.add(new Coordinate(i, j));
                    arrX.add(i);
                    arrY.add(j);
                }
            }
        }
        if (houses.size() == m * n) {
            return -1;
        }
        if (houses.size() == 0) {
            return 0;
        }
        Queue<Coordinate> queue = new LinkedList<Coordinate>();
        queue.offer(new Coordinate(getMedian(arrX), getMedian(arrY)));
        visited[getMedian(arrX)][getMedian(arrY)] = true;
        while(!queue.isEmpty()){
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Coordinate current = queue.poll();
                if (grid[current.x][current.y] == EMPTY) {
                    shortestPath = Math.min(shortestPath, getDistances(current, houses));
                }
                for (int dir = 0; dir < 4; dir++) {
                    Coordinate neighbor = new Coordinate(current.x + dirX[dir], current.y + dirY[dir]);
                    if (isInBound(grid, neighbor) && !visited[neighbor.x][neighbor.y]) {
                        queue.offer(neighbor);
                        visited[neighbor.x][neighbor.y] = true;
                    }
                }   
            }
        }
        if(shortestPath < Integer.MAX_VALUE){
            return shortestPath;
        }
        return -1;
    }

    private int getMedian(List<Integer> arr) {
        Collections.sort(arr);
        int median = arr.get(arr.size() / 2);
        if(arr.size() % 2 == 0){
            median = (median + arr.get(arr.size() / 2 - 1)) / 2;
        }
        return median;
    }

    private int getDistances(Coordinate cor, List<Coordinate> houses) {
        int distances = 0;
        for (Coordinate house : houses) {
            distances += Math.abs(house.x - cor.x) + Math.abs(house.y - cor.y);
        }
        return distances;
    }

    private boolean isInBound(int[][] grid, Coordinate cor) {
        return (cor.x >= 0 && cor.x < this.n && cor.y >= 0 && cor.y < this.m);
    }
}
```



