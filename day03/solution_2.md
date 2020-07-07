###  [矿泉水问题](<https://www.nowcoder.com/questionTerminal/7a1ae529644f4d94819a2a137d59d5c6?answerType=1&f=discussion>)

来源：[深信服校园招聘算法练习卷](<https://www.nowcoder.com/test/23358504/summary>)

小明横穿沙漠，需要携带至少x毫升的水。

有两种规格的矿泉水可供选购：小瓶矿泉水每瓶500ml，价格a元。大瓶矿泉水每瓶1500ml，价格b元。

小明打算买一些矿泉水用于横穿沙漠，为了保证至少买到x毫升的水，小明至少需要花费多少钱？

```
输入描述:
第一行一个正整数t(t<=1000)，表示有t组测试数据;

接下来t行，每行3个正整数：x，a，b。其中x<=1,000,000,000，表示小明至少需要x毫升水；a<=100，b<=100，分别表示小瓶和大瓶矿泉水的价格，单位：元。

输出描述:
每组测试数据输出一行，表示小明最少需要花费的钱，单位：元。
示例1
输入
3
5000 5 10
4999 5 10
5000 5 100
输出
35
35
50
```

- 贪心算法，根据价格的比较选择合适的容量，如果`3a<b`的话就直接所有全部买小瓶，否则需要考虑在小于1500ml时的选择。

```python
from math import ceil
def calc_min(x,a,b):
    money = 0
    if 3*a < b:
        buy_cnt = ceil(x / 500)
        money += buy_cnt * a
        
    else:
        buy_cnt = x // 1500
        x -= buy_cnt * 1500
        money += buy_cnt * b
        val1 = ceil(x/500)*a
        money += val1 if val1 < b else b
    return money

def main():
    N = int(input())
    for i in range(N):
        x,a,b = list(map(int,input().split()))
        print(calc_min(x,a,b))
        
main()
```

