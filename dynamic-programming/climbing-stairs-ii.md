# 272. Climbing Stairs II \[LintCode\]

> A child is running up a staircase with `n`steps, and can hop either 1 step, 2 steps, or 3 steps at a time. Implement a method to count how many possible ways the child can run up the stairs.
>
> **Example**
>
> n=`3`  
> 1+1+1=2+1=1+2=3=3
>
> return `4`

```java
public class Solution {
    /**
     * @param n an integer
     * @return an integer
     */
    public int climbStairs2(int n) {
        if (n <= 1) {
            return 1;
        }

        if (n == 2) {
            return 2;
        }

        int last = 1;
        int previous = 1;
        int now = 2;
        for (int i = 3; i <= n; i++) {
            int temp = now;
            now += last + previous;
            previous = last;
            last = temp;
        }

        return now;
    }
}
```



