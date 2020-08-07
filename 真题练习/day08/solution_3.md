### [社团主席选举](<https://www.nowcoder.com/practice/b8847dfb40964fa3aaaef6d2333938e4?tpId=122&&tqId=33719&rp=1&ru=/ta/exam-wangyi&qru=/ta/exam-wangyi/question-ranking>)

随着又一届学生的毕业，社团主席换届选举即将进行。

一共有n个投票者和m个候选人，小易知道每一个投票者的投票对象。但是，如果小易给某个投票者一些糖果，那么这个投票者就会改变他的意向，小易让他投给谁，他就会投给谁。

由于小易特别看好这些候选人中的某一个大神，这个人的编号是1，所以小易希望能尽自己的微薄之力让他当选主席，但是小易的糖果数量有限，所以请你帮他计算，最少需要花多少糖果让1号候选人当选。某个候选人可以当选的条件是他获得的票数比其他任何候选者都多。

```
输入描述:
第一行两个整数n和m，表示投票者的个数和候选人的个数。
接下来n行，每一行两个整数x和y，x表示这个投票者的投票对象，y表示需要花多少个糖果让这个人改变意向。
满足1 <= n, m <= 3000，1 <= x <= m，1 <= y <= 109。
输出描述:
一个整数，糖果的最小花费。
示例1
输入
1 2
1 20
输出
0
示例2
输入
5 5
2 5
3 5
4 5
5 6
5 1
输出
6
```

#### 分析

AC 60.暴力法，从所需糖数`x in [ceil(N/2),1]`开始遍历，每次计算时，大于`x-1`的部分都需要收买，之后如果不到`x`票，则排序选择最低的部分。

```python
from math import ceil

def calc_candies(need_ticket,price_dict):
    need_candies = 0
    cur_ticket = 0
    for supporter_prices in price_dict.values():
        if len(supporter_prices) >= need_ticket:
            supporter_prices.sort(key=lambda x:-x)
            while len(supporter_prices) >= need_ticket:
                need_candies += supporter_prices.pop()
                cur_ticket += 1
    if cur_ticket >= need_ticket:
        return need_candies
    rest_prices = []
    for supporter_prices in price_dict.values():
        rest_prices += supporter_prices
    if (need_ticket-cur_ticket) > len(rest_prices):
        return 1e9
    rest_prices.sort()
    for i in range(need_ticket-cur_ticket):
        need_candies += rest_prices[i]
    return need_candies
    
N,M = list(map(int,input().split()))
price_dict = {}
cur_ticket = 0
for _ in range(N):
    x,y = list(map(int,input().split()))
    if x == 1:
        cur_ticket += 1
        continue
    if x not in price_dict.keys():
        price_dict[x] = [y]
    else:
        price_dict[x].append(y)

min_candies = 1e9
for need_ticket in range(ceil(N/2),cur_ticket,-1):
    need_candies = calc_candies(need_ticket-cur_ticket,price_dict)
    min_candies = min(min_candies,need_candies)

print(min_candies) if min_candies!=1e9 else print(0)

```

