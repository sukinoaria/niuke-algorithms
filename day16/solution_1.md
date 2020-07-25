### [派分糖果](<https://www.nowcoder.com/practice/68ab121e08c5458fac5a22ec9964301a?tpId=155&&tqId=34011&rp=1&ru=/ta/exam-mogujie&qru=/ta/exam-mogujie/question-ranking>)

有N个孩子站成一排，每个孩子有一个分值。给这些孩子派发糖果，需要满足如下需求：

1、每个孩子至少分到一个糖果

2、分值更高的孩子比他相邻位的孩子获得更多的糖果

求至少需要分发多少糖果？

```
输入描述:
0,1,0
输出描述:
4
示例1
输入
5,4,1,1
输出
7
```

#### 分析

- 分两次遍历：从左到右以及从右到左

- 从左到右：初始情况下每个位置糖果为1，如果满足升序条件，其糖果数为上一个的糖果数加一
- 从右到左：找分数高但糖果数比右侧低的，将其值改为`max(candies[i],candies[i+1]+1)`。

```python
scores = list(map(int,input().split(',')))
candies = [1 for _ in range(len(scores))]

for i in range(1,len(scores)):
    if scores[i] > scores[i-1]:
        candies[i] = candies[i-1]+1

for i in range(len(scores)-2,-1,-1):
    if scores[i] > scores[i+1]:
        candies[i] = max(candies[i],candies[i+1]+1)
    
print(sum(candies))
```

