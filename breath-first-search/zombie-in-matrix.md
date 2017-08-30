# 598. Zombie in Matrix

> Given a 2D grid, each cell is either a wall 2, a zombie 1 or people 0 \(the number zero, one, two\).Zombies can turn the nearest people\(up/down/left/right\) into zombies every day, but can not through wall. How long will it take to turn all people into zombies? Return -1 if can not turn all people into zombies.
>
> **Example**
>
> Given a matrix:
>
> ```
> 0 1 2 0 0
> 1 0 0 2 1
> 0 1 0 0 0
>
> ```
>
> return `2`

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
     * @param grid  a 2D integer grid
     * @return an integer
     */
    public static final int PEOPLE = 0;
    public static final int ZOMBIE = 1;
    public static final int WALL = 2;
     
    public int zombie(int[][] grid) {
        // Write your code here
    
        if(grid == null || grid.length == 0 || grid[0].length == 0){
            return -1;
        }
        
        int[] dirX = new int[]{0, 0, 1, -1};
        int[] dirY = new int[]{1, -1, 0, 0};
        
        Queue<Coordinate> queue = new LinkedList<Coordinate>();
        int n = grid.length;
        int m = grid[0].length;
        int days = 0;
        int people = 0;
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(grid[i][j] == PEOPLE){
                    people++;
                }else if(grid[i][j] == ZOMBIE){
                    queue.offer(new Coordinate(i, j));
                }
            }
        }
        
        if(people == 0){
            return 0;
        }
        
        while(!queue.isEmpty()){
            days++;
            int size = queue.size();
            for(int i = 0; i < size; i++){
                Coordinate zombie = queue.poll();
                for(int j = 0; j < 4; j++){
                    Coordinate neighbor = new Coordinate(zombie.x + dirX[j], zombie.y + dirY[j]);
                    if(isPeople(grid, neighbor)){
                        queue.offer(neighbor);
                        grid[neighbor.x][neighbor.y] = ZOMBIE;
                        people--;
                        if(people == 0){
                            return days;
                        }
                    }
                }
            }
        }
        
        return -1;
    }
    
    private boolean isPeople(int[][] grid, Coordinate cor){
        
        int n = grid.length;
        int m = grid[0].length;
        
        if(cor.x >= 0 && cor.x < n && cor.y >= 0 && cor.y < m && grid[cor.x][cor.y] == PEOPLE){
            return true;
        }
        
        return false;
    }
    
}
```



