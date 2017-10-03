## 382. Triangle Count \[LintCode\]

> Given an array of integers, how many three numbers can be found in the array, so that we can build an triangle whose three edges length is the three numbers that we find?
>
> **Example**
>
> Given array S =`[3,4,6,7]`, return`3`. They are:
>
> ```
> [3,4,6]
> [3,6,7]
> [4,6,7]
> ```
>
> Given array S =`[4,4,4,4]`, return`4`. They are:
>
> ```
> [4(1),4(2),4(3)]
> [4(1),4(2),4(4)]
> [4(1),4(3),4(4)]
> [4(2),4(3),4(4)]
> ```

组成三角形的条件：两个小边之和大于第三边。

将数组排序后，问题变成Two Sum - Greater than target （巧妙）

```java
public class Solution {
    /**
     * @param S: A list of integers
     * @return: An integer
     */
    public int triangleCount(int S[]) {
        // write your code here
        if (S == null || S.length < 3) {
            return 0;
        }
        Arrays.sort(S);
        int count = 0;
        for (int i = 0; i < S.length; i++) {
            int target = S[i];
            int left = 0; 
            int right = i - 1;
            while (left < right) {
                if (S[left] + S[right] > target) {
                    count += right - left;
                    right--;
                } else {
                    left++;
                }
            }
        }
        return count;
    }
}
```



