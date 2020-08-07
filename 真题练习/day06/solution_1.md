### [骰子期望](<https://www.nowcoder.com/questionTerminal/86ef0d5042934ef7819035794377a507>)
来源：[拼多多2020校招部分编程题合集](<https://www.nowcoder.com/test/23354036/summary>)

扔n个骰子，第i个骰子有可能投掷出Xi种等概率的不同的结果，数字从1到Xi。所有骰子的结果的最大值将作为最终结果。求最终结果的期望。

```
输入描述:
第一行一个整数n，表示有n个骰子。（1 <= n <= 50）
第二行n个整数，表示每个骰子的结果数Xi。(2 <= Xi <= 50)

输出描述:
输出最终结果的期望，保留两位小数。
示例1
输入
2
2 2
输出
1.75
```

#### 分析

期望计算：
$$
E(X) = \sum_{k=1}^{K}p_kx_k
$$
对于该题，可以通过排列所有可能的情况来分析最大值分别取`1,2,...,n`的排列个数以及概率，从而求得最大值的期望。

最大值为`n`的排列个数：即第`n`个骰子固定为`n`,其他骰子任意值，共有`(n-1)*(n-2)*...*1`种。

- 注意对重复点数的骰子的处理方式：通过每次排序来得到点数最大值，其余值相乘得到该最大值出现的排列个数，之后要将该点数减一，从而计算更小的最大值的情况。

```python
N = int(input())
vals = list(map(int,input().split()))

# 所有可能的排列
all_times = 1
for val in vals:
    all_times *= val
    
#通过固定最大的骰子来确定该最大值的排列数，之后改数值减一，并重新排序
# 最大值等于1时停止，在计算总的情况时需要加1
res = 0
vals.sort()
while vals[-1] != 1:
    cur_times = 1
    for val in vals[:-1]:
        cur_times *= val
    # p_k * x_k
    res += vals[-1]*cur_times
    vals[-1] -= 1
    vals.sort()

print("%.2f" % float(res/all_times))
```

#### 解法二

- 思路：通过概率相减来得到：

$$
p(x=k) = p(x<=k) - p(x<=k-1)
$$

求多个骰子的联合概率分布的面积来得到最大值为`1,2,3...,n`的概率

![](https://wx2.sinaimg.cn/mw690/006dXJzOly1gglzfw5ktsj30no0fku0x.jpg)

```
对1来说，最大值为1 的概率就是1*1的正方形，概率为 1/2*1/3=1/6  
对2来说，最大值为2的概率就是2*2的正方形减去1*1的正方形 2/2*2/3-1/6 =3/6
对3来说，最大值为3的概率就是面积为6的长方形减去面积为4的，也就是2/2*3/3-4/6
```



```python
N = int(input())
vals = list(map(int,input().split()))

ans = 0
pre = 0
max_val = max(vals)
#循环遍历每个值作为最大值时的联合分布面积，并减去上一个最大值的面积
for i in range(1,max_val+1):
    cur = 1
    for j in range(N):
        # 确定 x <= i 可取的概率
        cur_val = min(i,vals[j])
        # N个骰子的联合概率
        cur *= cur_val / vals[j]
    # 当前最大值的概率，x_k * p_k 求解期望
    ans += (cur - pre)*i
    pre = cur
    
print("%.2f" % ans)
```

