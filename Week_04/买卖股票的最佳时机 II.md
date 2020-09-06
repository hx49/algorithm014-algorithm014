```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 1 ; i < prices.length ; i ++) {
            int tmp = prices[i] - prices[i - 1];
            if (tmp > 0) profit += tmp;
        }
        return profit;
    }
}
```

- 时间复杂度：O(n)
- 空间复杂度：O(1)