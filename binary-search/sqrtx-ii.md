# 586. Sqrt\(x\) II

> Implement`double sqrt(double x)`and`x >= 0`.
>
> Compute and return the square root of x.
>
> ##### Notice
>
> You do not care about the accuracy of the result, we will help you to output results.
>
>   
> **Example**

> Given`n`=`2`return`1.41421356`

```java
public class Solution {
    /**
     * @param x a double
     * @return the square root of x
     */
    public double sqrt(double x) {
        // Write your code here
        
        if(x == 0) return 0.0;
        
        double start = 0.0;
        double end = x;
        double mid;
        
        // special condition when < 1.0
        if(end < 1.0)
        {
            end = 1.0;
        }
        
        while(end - start > 1e-12)
        {
            mid = start + (end - start) / 2;
            
            if(mid * mid < x)
            {
                start = mid;
            }
            else
            {
                end = mid;
            }
        }
        return start;
    }
}
```



