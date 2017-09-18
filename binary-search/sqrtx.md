# 141. Sqrt\(x\) \[LintCode\]

> Implement int`sqrt(int x)`.
>
> Compute and return the square root of _x_.
>
> **Example**
>
> sqrt\(3\) = 1
>
> sqrt\(4\) = 2
>
> sqrt\(5\) = 2
>
> sqrt\(10\) = 3

本质是找平方之后尽可能接近x并且小于等于x的数，因此最后先判断end指针，再判断start指针

```java
public class Solution {
    /*
     * @param x: An integer
     * @return: The sqrt of x
     */
    public int sqrt(int x) {
        // write your code here
        if (x <= 0) {
            return 0;
        } 
        int start = 1;
        int end = x / 2 + 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (Math.pow(mid, 2) < x) {
                start = mid;
            } else if (Math.pow(mid, 2) > x) {
                end = mid;
            } else {
                return mid;
            }
        }
        if (Math.pow(end, 2) <= x) {
            return end;
        }
        return start;
    }
}
```



