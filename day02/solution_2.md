### 2. [倒卖战利品](https://www.nowcoder.com/questionTerminal/2f8a06421eea4dfe837453c8be6cb210?answerType=1&f=discussion)
来源：[小红书2020校招算法笔试题卷二](<https://www.nowcoder.com/test/23568060/summary>)

在游戏中，击败魔物后，薯队长获得了N件宝物，接下来得把这些宝物卖给宝物回收员来赚点小钱。这个回收员有个坏毛病，每次卖给他一件宝 物后，之后他就看不上比这件宝物差的宝物了。在这个世界中，衡量宝物的好坏有两个维度，稀有度X和实用度H，回收员在回收一个宝物A 后，下一个宝物的稀有度和实用度都不能低于宝物A。那么薯队长如何制定售卖顺序，才能卖给回收员宝物总个数最多。 

```
输入描述:
第一行一个正整数N。 接下来N行。每行两个整数分别表示X和H.(X1 H1,X2 H2, …,XN,HN)
输入限制： 对于70%的数据： 
0<N<10^4 
0<Xi<10^6 
0<Hi<10^6 
100%的数据：
0<N<10^6
0<Xi<10^6 
0<Hi<10^6

输出描述:
一个整数，表示最多可以卖出的宝物数
示例1
输入
4
3 2
1 1 
1 3
1 2
输出
3
```

#### 分析

- 思路 先对数组排序(`sort`函数会同时对两个维度排序，第一个维度相同时会比较第二个维度)，然后在另一个维度上搜索最长上升子序列。

```python
input: [[3 2],[1 1],[1 3],[1 2]]
sorted(input):[[1 1],[1 2],[1 3],[3 2]]
```

- 时间复杂度的限制：在找最长上升子序列时不能使用DP方法(`O(N^2)`)，考虑通过二分查找来找到LIS。
- **LIS的二分查找算法**：[参考: leetcode 300.最长上升子序列](<https://leetcode-cn.com/problems/longest-increasing-subsequence/solution/zui-chang-shang-sheng-zi-xu-lie-by-leetcode-soluti/>)
  - 构造单调上升数组`res`，对原数组`nums`逐个遍历：
    - 如果`nums[i]>res[-1]`，说明满足上升条件，将其插入数组中；
    - 否则，通过二分查找`res`数组中刚好比它大的值并进行替换。**当完成多次替换后该数组的最大值会减小，从而能向res中添加一些原数组中较小的值。**
  - 计算数组的长度得到LIS的最大值。
- 注意二分搜索时的边界以及返回值选择

```python
def binary_search(nums,left,right,val):
    mid = 0
    while left < right:
        mid = (left+right) // 2
        if val > nums[mid]:
            left = mid +1
        else:
            right = mid
    return left
 
def LIS(N,prices):
    res = []
    for i in range(N):
        if not res or prices[i] > res[-1]:
            res.append(prices[i])
        else:
            idx = binary_search(res, 0, len(res), prices[i])
            res[idx] = prices[i]
    return len(res)
         
def main():
    N = int(input())
    prices = []
    for i in range(N):
        prices.append(list(map(int,input().split())))
    prices.sort()
    h = [a[1] for a in prices]
    return LIS(N,h)
     
print(main())
```

