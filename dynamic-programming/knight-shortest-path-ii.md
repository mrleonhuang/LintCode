# 630. Knight Shortest Path II \[LintCode\]

> Given a knight in a chessboard `n * m`\(a binary matrix with 0 as empty and 1 as barrier\). the knight initialze position is`(0, 0)`and he wants to reach position`(n - 1, m - 1)`, Knight can only be from left to right. Find the shortest path to the destination position, return the length of the route. Return`-1`if knight can not reached.
>
> **Clarification**
>
> If the knight is at \(x, y\), he can get to the following positions in one step:
>
> ```
> (x + 1, y + 2)
> (x - 1, y + 2)
> (x + 2, y + 1)
> (x - 2, y + 1)
> ```
>
> **Example**
>
> ```
> [[0,0,0,0],
>  [0,0,0,0],
>  [0,0,0,0]]
>
> Return 3
>
> [[0,0,0,0],
>  [0,0,0,0],
>  [0,1,0,0]]
>
> Return -1
> ```

* **与Knight Shortest Path I 不同点在于这道题规定了骑士必须从左往右走，有方向性才能用DP！！**

* **坐标型DP开数组不用 +1 ！！**

* **对于每一个坐标点，找能跳到本坐标点的前一个坐标，如果前一个坐标可达，则**

  ```java
         dp[i][j] = Math.min(dp[i][j], pre-step-dp[i][j] + 1);
  ```

* **错误点：递推的顺序要注意，从左到右，因此第一层遍历 j 第二层才遍历 i 并且 j 从1开始**

```java
public class Solution {
    /**
     * @param grid a chessboard included 0 and 1
     * @return the shortest path
     */
    private int n;
    private int m;

    public int shortestPath2(boolean[][] grid) {
        // Write your code here
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return -1;
        }
        this.n = grid.length;
        this.m = grid[0].length;
        // dp[i][j] means the shortest path from grid[0][0]
        int[][] dp = new int[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                dp[i][j] = Integer.MAX_VALUE;
            }
        }
        dp[0][0] = 0;
        for (int j = 1; j < m; j++) {
            for (int i = 0; i < n; i++) {
                if (grid[i][j]) {
                    continue;
                }
                if (inBound(i - 1, j - 2) && dp[i - 1][j - 2] != Integer.MAX_VALUE) {
                    dp[i][j] = Math.min(dp[i][j], dp[i - 1][j - 2] + 1);
                } 
                if (inBound(i + 1, j - 2) && dp[i + 1][j - 2] != Integer.MAX_VALUE) {
                    dp[i][j] = Math.min(dp[i][j], dp[i + 1][j - 2] + 1);
                }
                if (inBound(i - 2, j - 1) && dp[i - 2][j - 1] != Integer.MAX_VALUE) {
                    dp[i][j] = Math.min(dp[i][j], dp[i - 2][j - 1] + 1);
                }
                if (inBound(i + 2, j - 1) && dp[i + 2][j - 1] != Integer.MAX_VALUE) {
                    dp[i][j] = Math.min(dp[i][j], dp[i + 2][j - 1] + 1);
                }
            }
        }
        if (dp[n - 1][m - 1] == Integer.MAX_VALUE) {
            return -1;
        }
        return dp[n - 1][m - 1];
    }

    private boolean inBound(int x, int y) {
        return x >= 0 && x < n && y >= 0 && y < m;
    }
}
```



