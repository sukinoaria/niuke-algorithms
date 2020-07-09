### [多多的排列函数](<https://www.nowcoder.com/questionTerminal/b78a667f19134c798a330a8f1432e1d5>)

来源：[拼多多2020校招部分编程题合集](<https://www.nowcoder.com/test/23354036/summary>)

数列 {An} 为N的一种排列。
例如N=3，可能的排列共6种：

```
1, 2, 3
1, 3, 2
2, 1, 3
2, 3, 1
3, 1, 2
3, 2, 1
```

定义函数F:
$$
dp[i][j] = \begin{cases}  
A_1 & x=1 \\
|F(x-1)-A_x| & x>1
\end{cases}
$$
其中|X|表示X的绝对值。

现在多多鸡想知道，在所有可能的数列 {An} 中，F(N)的最小值和最大值分别是多少。

```
输入描述:
第一行输入1个整数T，表示测试用例的组数。
( 1 <= T <= 10 )
第二行开始，共T行，每行包含1个整数N，表示数列 {An} 的元素个数。
( 1 <= N <= 100,000 )
输出描述:
共T行，每行2个整数，分别表示F(N)最小值和最大值
示例1
输入
2
2
3
输出
1 1
0 2
说明
对于N=3：

- 当{An}为3，2，1时可以得到F(N)的最小值0
- 当{An}为2，1，3时可以得到F(N)的最大值2

备注:
对于60%的数据有： 1 <= N <= 100
对于100%的数据有：1 <= N <= 100,000
```

#### 分析

对最小值的求解，当数组是上升或者下降的时候均满足，其值只能是1或者0,通过函数`calc_min()`直接计算。

最大值的求解，不能通过回溯去生成序列(时间复杂度太高),由函数`F`的公式：$F(x)=|F(x-1)-A_x|$，要使得`F(x)`最大，即令`F(x-1)`最小，即`N - calc_min(N-1)`。

```python
def calc_min(N):
    min_li = [i for i in range(N,0,-1)]
    res = min_li[0]
    for i in range(1,N):
        res = abs(res-min_li[i])
    return res

def calc_min_max(N):
    min_val = calc_min(N)
    max_val = N - calc_min(N-1)
    print("{} {}".format(min_val,max_val))
    
def main():
    T = int(input())
    for i in range(T):
        N = int(input())
        if N == 1:
            print("1 1")
        else:
            calc_min_max(N)
main()
```

