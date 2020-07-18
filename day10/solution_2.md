### [最小代价爬楼梯](<https://www.nowcoder.com/practice/355885694012495281f415387db22fde?tpId=131&&tqId=33836&rp=1&ru=/ta/exam-kuaishou&qru=/ta/exam-kuaishou/question-ranking>)

你需要爬上一个N层的楼梯，在爬楼梯过程中， 每阶楼梯需花费非负代价，第i阶楼梯花费代价表示为cost[i]， 一旦你付出了代价，你可以在该阶基础上往上爬一阶或两阶。
你可以从第 0 阶或者 第 1 阶开始，请找到到达顶层的最小的代价是多少。
N和cost[i]皆为整数，且N∈[2,1000]，cost[i]∈ [0, 999]。

```
输入描述:
输入为一串半角逗号分割的整数，对应cost数组，例如

10,15,20
输出描述:
输出一个整数，表示花费的最小代价
示例1
输入
1,100,1,1,1,100,1,1,100,1
输出
6
```

#### 分析

动态规划，从第0个位置和第1个位置出发都是0，之后转移方程：

`f(i) = min(f(i-1)+nums[i-1],f(i-2)+nums[i-2])`

```python
nums = list(map(int,input().split(',')))

dp = [0] * (len(nums)+1)
#dp[0] = nums[0]
#dp[1] = min(nums[0],nums[1])

for i in range(2,len(nums)+1):
    dp[i] = min(dp[i-1]+nums[i-1],dp[i-2]+nums[i-2])
print(dp[-1])
```

