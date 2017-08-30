# 600. Smallest Rectangle Enclosing Black Pixels

> An image is represented by a binary matrix with `0 `as a white pixel and `1 `as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location`(x, y)`of one of the black pixels, return the area of the smallest \(axis-aligned\) rectangle that encloses all black pixels.
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
>
> ```
>
> and x =`0`, y =`2`,  
> Return`6`.

```java
public class Solution {
    /**
     * @param image a binary matrix with '0' and '1'
     * @param x, y the location of one of the black pixels
     * @return an integer
     */
    public int minArea(char[][] image, int x, int y) {
        // Write your code here
        
        if(image == null || image.length == 0) return 0;
        if(image[0] == null || image[0].length == 0) return 0;
        
        int M = image[0].length;
        int N = image.length;
        int left = 0;
        int right = 0;
        int up = 0;
        int bottom = 0;
        
        // find the left bound
        int start = 0;
        int end = y;
        int mid;
        while(start + 1 < end)
        {
            mid = start + (end - start) / 2;
            
            if(colHasBlackPixel(image, mid))
            {
                end = mid;
            }
            else
            {
                start = mid;
            }
        }
        if(colHasBlackPixel(image, start)) left = start;
        else if(colHasBlackPixel(image, end)) left = end;
        else return 0;
        
        // find the right bound
        start = y;
        end = M - 1;
        while(start + 1 < end)
        {
            mid = start + (end - start) / 2;
            
            if(colHasBlackPixel(image, mid))
            {
                start = mid;
            }
            else
            {
                end = mid;
            }
        }
        if(colHasBlackPixel(image, end)) right = end;
        else if(colHasBlackPixel(image, start)) right = start;
        else return 0;
        
        // find the up bound
        start = 0;
        end = x;
        while(start + 1 < end)
        {
            mid = start + (end - start) / 2;
            
            if(rowHasBlackPixel(image, mid))
            {
                end = mid;
            }
            else
            {
                start = mid;
            }
        }
        if(rowHasBlackPixel(image, start)) up = start;
        else if(rowHasBlackPixel(image, end)) up = end;
        else return 0;
        
        // find the bottom bound
        start = x;
        end = N - 1;
        while(start + 1 < end)
        {
            mid = start + (end - start) / 2;
            
            if(rowHasBlackPixel(image, mid))
            {
                start = mid;
            }
            else
            {
                end = mid;
            }
        }
        if(rowHasBlackPixel(image, end)) bottom = end;
        else if(rowHasBlackPixel(image, start)) bottom = start;
        else return 0;
        
        return (right - left + 1) * (bottom - up + 1);
        
    }
    
    private boolean colHasBlackPixel(char[][] image, int col)
    {   
        if(image == null || col < 0) return false;
        
        for(int i = 0; i < image.length; i++)
        {
            if(image[i][col] == '1') return true;
        }
        return false;
    }
    
    private boolean rowHasBlackPixel(char[][] image, int row)
    {
        if(image == null || row < 0) return false;
        
        for(int i = 0; i < image[0].length; i++)
        {
            if(image[row][i] == '1') return true;
        }
        return false;
    }
}
```



