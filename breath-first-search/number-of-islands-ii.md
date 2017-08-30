# 434. Number of Islands II

> Given a n,m which means the row and column of the 2D matrix and an array of pair A\( size k\). Originally, the 2D matrix is all 0 which means there is only sea in the matrix. The list pair has k operator and each operator has two integer A\[i\].x, A\[i\].y means that you can change the grid matrix\[A\[i\].x\]\[A\[i\].y\] from sea to island. Return how many island are there in the matrix after each operator.
>
> ##### Notice
>
> 0 is represented as the sea, 1 is represented as the island. If two 1 is adjacent, we consider them in the same island. We only consider up/down/left/right adjacent.
>
> **Example**
>
> Given`n`=`3`,`m`=`3`, array of pair A =`[(0,0),(0,1),(2,2),(2,1)]`.
>
> return`[1,1,2,2]`.

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
public class Solution {
    /**
     * @param n an integer
     * @param m an integer
     * @param operators an array of point
     * @return an integer array
     */
    public List<Integer> numIslands2(int n, int m, Point[] operators) {
        // Write your code here
    }
}
```



