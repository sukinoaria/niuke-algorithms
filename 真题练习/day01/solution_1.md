### [笔记精选](<https://www.nowcoder.com/questionTerminal/60a9ce2437694f4f81d6ed94a0c265e9?answerType=1&f=discussion>)
来源：[小红书2020校招算法笔试题卷一](<https://www.nowcoder.com/test/23568027/summary>)

> 时间限制：C/C++ 1秒，其他语言2秒
>
> 空间限制：C/C++ 256M，其他语言512M

 薯队长写了n篇笔记，编号从1~n,每篇笔记都获得了不少点赞数。    

薯队长想从中选出一些笔记，作一个精选集合。挑选的时候有两个规则：

- 1.不能出现连续编号的笔记。 

- 2.总点赞总数最多 

如果满足1，2条件有多种方案，挑选笔记总数最少的那种

```
输入描述:
输入包含两行。第一行整数n表示多少篇笔记。 第二行n个整数分别表示n篇笔记的获得的点赞数。   
（0<n<=1000, 0<=点赞数<=1000) 

输出描述:
输出两个整数x,y。空格分割。
x表示总点赞数，y表示挑选的笔记总数。

输入例子1:
4
1 2 3 1

输出例子1:
4 2
```

---

### 分析

考察点：动态规划

相比于经典的[打家劫舍问题](<https://leetcode-cn.com/problems/house-robber/>)，多了个对选择的个数的限制。对每个位置的状态用`dp_star[i]`来表示在`[0,i]`上能获得的最大点赞数。在计算总点赞数数组`dp_star`的基础上，多加一个动态规划数组`dp_count`来统计在每个位置`i`上取到最大点赞数时的笔记的个数。

最大点赞数数组的状态转移方程为：`f(i) = max(f(j)+nums[i],f(i-1)), j in [0,i-2]`

其中`j in[0,i-2]​`是取`i`处的笔记时的最大点赞数，还要与不取`i`处的笔记时的最大点赞总数`dp_star[i-1]`进行比较，取最大的为当前点赞数，如果最大值是取了当前位置的笔记得到的，那么笔记的计数也需要加一。

```python
N = int(input())
nums = list(map(int, input().split()))

def getMaxStar(N, nums):
    dp_star = [0 for _ in range(N)]
    dp_count = [0 for _ in range(N)]
    dp_star[0], dp_count[0] = nums[0], 1
    dp_star[1], dp_count[1] = nums[1] if nums[1] > nums[0] else nums[0], 1
    for i in range(2, N):
        # get nums[i]
        for j in range(0, i-1):
            if dp_star[j] + nums[i] > dp_star[i]:
                dp_star[i] = dp_star[j] + nums[i]
                dp_count[i] = dp_count[j] + 1
        # not get nums[i], compare dp_star[i-1]
        if dp_star[i-1] > dp_star[i]:
            dp_star[i] = dp_star[i-1]
            dp_count[i] = dp_count[i-1]
    # get max star num with min count
    max_val, min_cnt = 0, 10000
    for val, cnt in zip(dp_star, dp_count):
        if val > max_val:
            max_val = val
            min_cnt = cnt
        elif val == max_val:
            if cnt < min_cnt:
                min_cnt = cnt

    print(max_val, min_cnt)

getMaxStar(N,nums)
```

