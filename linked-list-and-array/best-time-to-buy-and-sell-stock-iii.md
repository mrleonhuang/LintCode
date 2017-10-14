## 123. Best Time to Buy and Sell Stock III

> Say you have an array for which theithelement is the price of a given stock on dayi.
>
> Design an algorithm to find the maximum profit. You may complete at mosttwotransactions.
>
> **Note:**  
> You may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

最多允许2次买卖，并且同一时间只能持有一支股票。

思路是找到时间跨度中任意一点作为分割点，该分割点两边分别拥有两支。遍历所有时间节点，找出最大的那个就是最大利润。

针对任意一个时间节点，算法是从数组的两头分别进行计算：第一遍从头到尾跟 I 的方法一样，本质是计算**如果在该点卖出，能得到的最大收益。**第二遍从尾到头，本质是计算**如果在该点买入，能得到的最大收益。**两段相加，则为该点作为分割点的最大收益。

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) {
            return 0;
        }
        int[] profits = new int[prices.length];
        int maxProfit = 0;
        int minPrice = prices[0];
        for (int i = 0; i < prices.length; i++) {
            maxProfit = Math.max(maxProfit, prices[i] - minPrice);
            profits[i] = maxProfit;
            minPrice = Math.min(minPrice, prices[i]);
        }
        maxProfit = 0;
        int maxPrice = prices[prices.length - 1];
        for (int i = prices.length - 1; i >= 0; i--) {
            maxProfit = Math.max(maxProfit, maxPrice - prices[i]);
            profits[i] += maxProfit;
            maxPrice = Math.max(maxPrice, prices[i]);
        }
        maxProfit = 0;
        for (int i = 0; i < profits.length; i++) {
            maxProfit = Math.max(maxProfit, profits[i]);
        }
        return maxProfit;
    }
}
```

本题跟第一题一样，用趋势法能通过大部分的case，但是有些special cases是过不了的。比如\[1,2,4,2,5,7,2,4,9,0\]

```java
// WRONG ANSWER !!!
// but good thought
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) {
            return 0;
        }
        PriorityQueue<Integer> profits = new PriorityQueue<Integer>(3, Collections.reverseOrder());
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
            profits.offer(prices[sell] - prices[buy]);
        }
        i = 0;
        int maxProfit = 0;
        while (!profits.isEmpty() && i < 2) {
            maxProfit += (int) profits.poll();
            i++;
        }
        return maxProfit;
    }
}
```



