## 183. Wood Cut

> Given n pieces of wood with length`L[i]`\(integer array\). Cut them into small pieces to guarantee you could have equal or more than k pieces with the same length. What is the longest length you can get from the n pieces of wood? Given L & k, return the maximum length of the small pieces.
>
> ##### Notice
>
> You couldn't cut wood into float length.
>
> If you couldn't get &gt;=\_k \_pieces, return`0`.
>
> **Example**
>
> For`L=[232, 124, 456]`,`k=7`, return`114`.

算法本身很简单，纯二分搜索。注意二分搜索的right指针是最长的木板（相当于丢弃掉除最长板之外的其他板），不是最短的木板。

```java
public class Solution {
    /*
     * @param L: Given n pieces of wood with length L[i]
     * @param k: An integer
     * @return: The maximum length of the small pieces
     */
    public int woodCut(int[] L, int k) {
        // write your code here
        if (L == null || L.length == 0 || k <= 0) {
            return 0;
        }
        int longest = Integer.MIN_VALUE;
        for (int i = 0; i < L.length; i++) {
            longest = Math.max(longest, L[i]);
        }
        int start = 1;
        int end = longest;
        int mid;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (getPieces(L, mid) < k) {
                end = mid;
            } else if (getPieces(L, mid) >= k) {
                start = mid;
            } 
        }
        if (getPieces(L, end) >= k) {
            return end;
        }
        if (getPieces(L, start) >= k) {
            return start;
        }
        return 0;
    }

    private int getPieces(int[] L, int length) {
        int pieces = 0;
        for (int i = 0; i < L.length; i++) {
            pieces += L[i] / length;
        }
        return pieces;
    }
}
```



