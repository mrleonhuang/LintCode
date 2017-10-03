## 612. K Closest Points \[LintCode\]

> Given some
>
> `points`and a point `origin`in two dimensional space, find `k`points out of the some points which are nearest to `origin`. Return these points sorted by distance, if they are same with distance, sorted by x-axis, otherwise sorted by y-axis.
>
> **Example**
>
> Given points =`[[4,6],[4,7],[4,4],[2,5],[1,1]]`, origin =`[0, 0]`, k =`3`  
> return`[[1,1],[2,5],[4,4]]`

计算每一个点到origin点的距离，然后扔进最大堆，如果距离相等，按照x的距离和y的距离排序。

* 根据不同特点来进行排序（比如这道题的距离，x坐标，y坐标），用comparator来实现

* 注意Comparator里两个参数比较的意义，pair2 - pair2是相当于把大数扔到堆顶准备扔掉

* 从Heap或者PriorityQueue中往数组里传结果一定注意顺序，poll出来的是大数还是小数，应该放在数组的前面还是后面

* 坐标距离计算要注意是是勾股定理不用开根号，\(x1-x2\)\*\(x1-x2\) + \(y1-y2\)\*\(y1-y2\) 求绝对距离还是用Math.abs\(x1-x2\) + Math.abs\(y1-y2\)求行走距离

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
class Pair {
    Point point; 
    int dist;
    public Pair(Point point, int dist) {
        this.point = point;
        this.dist = dist;
    }
} 

public class Solution {
    /**
     * @param points a list of points
     * @param origin a point
     * @param k an integer
     * @return the k closest points
     */
    public Point[] kClosest(Point[] points, Point origin, int k) {
        // Write your code here
        if (points == null || points.length == 0 || points.length < k) {
            return new Point[0];
        }
        PriorityQueue<Pair> maxHeap = new PriorityQueue<Pair>(k + 1, new Comparator<Pair>(){
            public int compare(Pair p1, Pair p2) {
                if (p1.dist != p2.dist) {
                    return p2.dist - p1.dist;
                } else if (p1.point.x != p2.point.x) {
                    return p2.point.x - p1.point.x;
                }
                return p2.point.y - p1.point.y;
            }
        });
        for (Point point : points) {
            Pair newPair = new Pair(point, getDistance(origin, point));
            maxHeap.offer(newPair);
            if (maxHeap.size() == k + 1) {
                maxHeap.poll();
            }
        }
        Point[] results = new Point[k];
        for (int i = k - 1; i >= 0; i--) {
            results[i] = maxHeap.poll().point;
        }
        return results;
    }

    private int getDistance(Point origin, Point p) {
        return (p.x - origin.x) * (p.x - origin.x) + (p.y - origin.y) * (p.y - origin.y);
    }
}
```



