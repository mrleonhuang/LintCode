## 122. Best Time to Buy and Sell Stock II

> Say you have an array for which theithelement is the price of a given stock on dayi.
>
> Design an algorithm to find the maximum profit. You may complete as many transactions as you like \(ie, buy one and sell one share of the stock multiple times\). However, you may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

1. Greedy算法，遍历数组，遇到后一个点大于前一个点，就加入profit总和。这个算法虽然算出来的结果是正确的，但是违反了题目一天只能有一次交易的原则。
2. 按照趋势图的思维，找到任意一段上升趋势，则加入总profit

```java
class Solution {
    public int maxProfit(int[] prices) {
          if (prices == null || prices.length < 2) {
            return 0;
        }
        int maxProfit = 0;
        int i = 1;
        while (i < prices.length) {
            int buy, sell;
            while (i < prices.length && prices[i - 1] >= prices[i]) {
                i++;
            }
            buy = i - 1;
            while (i < prices.length && prices[i - 1] <= prices[i]) {
                i++;
            }
            sell = i - 1;
            maxProfit += prices[sell] - prices[buy];
        }
        return maxProfit;
    }
}
```





