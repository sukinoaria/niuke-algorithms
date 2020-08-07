### [ 风口的猪 - 中国牛市](<https://www.nowcoder.com/practice/9370d298b8894f48b523931d40a9a4aa?tpId=125&&tqId=33730&rp=1&ru=/ta/exam-xiaomi&qru=/ta/exam-xiaomi/question-ranking>)

风口之下，猪都能飞。当今中国股市牛市，真可谓“错过等七年”。 给你一个回顾历史的机会，已知一支股票连续n天的价格走势，以长度为n的整数数组表示，数组中第i个元素（prices[i]）代表该股票第i天的股价。 假设你一开始没有股票，但有至多两次买入1股而后卖出1股的机会，并且买入前一定要先保证手上没有股票。若两次交易机会都放弃，收益为0。 设计算法，计算你能获得的最大收益。 

```
输入数值范围：2<=n<=100,0<=prices[i]<=100
示例1
输入
3,8,5,1,7,8
输出
12
```

[参考方法：一个方法团灭6道股票问题](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/solution/yi-ge-fang-fa-tuan-mie-6-dao-gu-piao-wen-ti-by-l-3/)

状态转移：

- `i`为日期，`k`为当前交易次数，`0`和`1`分别代表这一天是否持有股票。
- `k`的变化：每当买了股票后减一，卖出时不做处理。

```python
dp[i][k][0] = max( dp[i-1][k][0] ，dp[i-1][k][1]+price[i] )
#第i天，还剩余k次交易次数，且当前不持有股票，其最大收益：昨天就不持有、昨天持有今日卖出的最大值。

dp[i][k][1] = max( dp[i-1][k][1] ，dp[i-1][k-1][0]-price[i] )
#第i天，还剩余k次交易次数，且持有股票，其最大收益：昨天就持有、今日购买的最大值。
#k和k-1同时出现，后面的会依赖前面的，因此在压缩存储空间时要倒着对k进行遍历。
```

- 初始情况：

```python
dp[-1][k][0]:    #初始情况下不持有股票，收益为0
dp[-1][k][1]:    #负无穷，该情况不可能持有股票
```

- 其他情况：当交易次数>天数/2时，即每天交换也不会超过次数限制，相当于没有交易次数限制，直接可以贪心法计算每天的增量收益加起来。

- 牛客的系统好像有问题

```java
public class Solution {
    /**
     * 计算你能获得的最大收益
     *
     * @param prices Prices[i]即第i天的股价
     * @return 整型
     */
    public int calculateMax(int[] prices) {
        int k = 2;
        int[] dp_ik_0 = new int[k+1];
        int[] dp_ik_1 = new int[k+1];
        for (int i = 0;i<k+1;i++)
            dp_ik_1[i] = Integer.MIN_VALUE;
        for (int i =0;i<prices.length;i++)
        {
            for (int j = k;j>0;j--)
            {
                dp_ik_0[j] = Math.max(dp_ik_0[j],dp_ik_1[j]+ prices[i]);
                dp_ik_1[j] = Math.max(dp_ik_1[j],dp_ik_0[j-1] - prices[i]);
            }
        }
        return dp_ik_0[k];
    }
}
```

