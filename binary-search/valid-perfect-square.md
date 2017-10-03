## 367. Perfect Valid Square \[LeetCode\]

> Given a positive integernum, write a function which returns True ifnumis a perfect square else False.
>
> **Note:Do not**use any built-in library function such as`sqrt`.
>
> **Example 1:**
>
> ```
> Input: 16
> Returns: True
> ```
>
> **Example 2:**
>
> ```
> Input: 14
> Returns: False
> ```

* 涉及平方数的时候要考虑int\(2^32\)是否够用，尽量用long\(2^64\)
* Math.pow会自动生成double型
* long和int可以直接比较不需要cast

```java
class Solution {
    public boolean isPerfectSquare(int num) {
        long start = 1;
        long end = num / 2 + 1;
        long mid;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (mid * mid < num) {
                start = mid;
            } else if (mid * mid > num) {
                end = mid;
            } else {
                return true;
            }
        }
        if (start * start == num || end * end == num) {
            return true;
        }
        return false;
    }
}
```



