# 586. Sqrt\(x\) II

> Implement`double sqrt(double x)`and`x >= 0`.
>
> Compute and return the square root of x.
>
> ##### Notice
>
> You do not care about the accuracy of the result, we will help you to output results.
>
> **Example**
>
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
        if(end < 1.0) {
            end = 1.0;
        }
        while(end - start > 1e-12) {
            // 二分浮点数 和二分整数不同
            // 一般都有一个精度的要求 譬如这题就是要求小数点后八位
            // 也就是只要我们二分的结果达到了这个精度的要求就可以
            // 所以 需要让 right 和 left 小于一个我们事先设定好的精度值 eps
            // 一般eps的设定1e-8,因为这题的要求是到1e-8,所以我把精度调到了1e-12
            // 最后 选择 left 或 right 作为一个结果即可 
            mid = (start + end) / 2;
            if(mid * mid < x) {
                start = mid;
            } else {
                end = mid;
            }
        }
        return start;
    }
}
```



