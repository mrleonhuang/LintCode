## 600. Smallest Rectangle Enclosing Black Pixels \[LintCode\]

> An image is represented by a binary matrix with `0`as a white pixel and `1`as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location`(x, y)`of one of the black pixels, return the area of the smallest \(axis-aligned\) rectangle that encloses all black pixels.
>
> **Example**
>
> For example, given the following image:
>
> ```
> [
>   "0010",
>   "0110",
>   "0100"
> ]
> ```
>
> and x =`0`, y =`2`,  
> Return`6`.

往四个方向进行二分搜索，注意往不同方向搜索的时候，指针的调整规律不一样。

```java
public class Solution {
    /*
     * @param image: a binary matrix with '0' and '1'
     * @param x: the location of one of the black pixels
     * @param y: the location of one of the black pixels
     * @return: an integer
     */
    public int minArea(char[][] image, int x, int y) {
        // write your code here
        if (image == null || image.length == 0 || image[0].length == 0) {
            return 0;
        }
        int leftBound = findLeftBound(image, 0, y);
        int rightBound = findRightBound(image, y, image[0].length - 1);
        int upperBound = findUpperBound(image, 0, x);
        int lowerBound = findLowerBound(image, x, image.length - 1);
        return (rightBound - leftBound + 1) * (lowerBound - upperBound + 1);
    }

    private int findLeftBound(char[][] image, int left, int right) {
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (existBlackInCol(image, mid)) {
                right = mid;
            } else {
                left = mid;
            }
        }
        if (existBlackInCol(image, left)) {
            return left;
        }
        return right;
    }

    private int findRightBound(char[][] image, int left, int right) {
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (existBlackInCol(image, mid)) {
                left = mid;
            } else {
                right = mid;
            }
        }
        if (existBlackInCol(image, right)) {
            return right;
        }
        return left;
    }

    private int findUpperBound(char[][] image, int up, int down) {
        while (up + 1 < down) {
            int mid = up + (down - up) / 2;
            if (existBlackInRow(image, mid)) {
                down = mid;
            } else {
                up = mid;
            }
        }
        if (existBlackInRow(image, up)) {
            return up;
        }
        return down;
    }

    private int findLowerBound(char[][] image, int up, int down) {
        while (up + 1 < down) {
            int mid = up + (down - up) / 2;
            if (existBlackInRow(image, mid)) {
                up = mid;
            } else {
                down = mid;
            }
        }
        if (existBlackInRow(image, down)) {
            return down;
        }
        return up;
    }

    private boolean existBlackInCol(char[][] image, int y) {
        for (int i = 0; i < image.length; i++) {
            if (image[i][y] == '1') {
                return true;
            }
        }
        return false;
    }

    private boolean existBlackInRow(char[][] image, int x) {
        for (int i = 0; i < image[0].length; i++) {
            if (image[x][i] == '1') {
                return true;
            }
        }
        return false;
    }
}
```



