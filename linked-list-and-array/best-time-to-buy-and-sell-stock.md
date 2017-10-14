## 121. Best Time to Buy and Sell Stock

> Say you have an array for which theithelement is the price of a given stock on dayi.
>
> If you were only permitted to complete at most one transaction \(ie, buy one and sell one share of the stock\), design an algorithm to find the maximum profit.
>
> **Example 1:**
>
> ```
> Input: [7, 1, 5, 3, 6, 4]
> Output: 5
>
> max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
>
> ```
>
>
>
> **Example 2:**
>
> ```
> Input: [7, 6, 4, 3, 1]
> Output: 0
>
> In this case, no transaction is done, i.e. max profit = 0.
> ```

遍历价格数组，找到截止到当前点为止的最小价格，并且算出截止到当前点最大利润。如果用趋势图的思维，就是找历史最低点和历史最高点。

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length < 2) {
            return 0;
        }
        int maxProfit = 0;
        int minPrice = prices[0];
        for (int i = 0; i < prices.length; i++) {
            maxProfit = Math.max(maxProfit, prices[i] - minPrice);
            minPrice = Math.min(minPrice, prices[i]);
        }
        return maxProfit;
    }
}
```



