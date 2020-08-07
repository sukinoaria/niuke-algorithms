### [二维表第k大数](<https://www.nowcoder.com/questionTerminal/98929bfe8f6b4beba5838285ae99aa6f>)

来源：[拼多多2020校招部分编程题合集](<https://www.nowcoder.com/test/23354036/summary>)

在一块长为n，宽为m的场地上，有`n*m`个`1*1`的单元格。每个单元格上的数字就是按照从1到n和1到m中的数的乘积。具体如下

```
n = 3, m = 3
1   2   3
2   4   6
3   6   9
```

给出一个查询的值k，求出按照这个方式列举的的数中第k大的值v。

```
例如上面的例子里，
从大到小为(9, 6, 6, 4, 3, 3, 2, 2, 1)
k = 1, v = 9
k = 2, v = 6
k = 3, v = 6
...
k = 8, v = 2
k = 9, v = 1
```

```
输入描述:
只有一行是3个数n, m, k 表示场地的宽高和需要查询的k。使用空格隔开。

输出描述:
给出第k大的数的值。
示例1
输入
3 3 4
输出
4

备注:
【数据范围】
100%的数据
1 <= n, m <= 40000
1 <= k <= n * m
30%的数据
1 <= n, m <= 1000
```

#### 分析

- 思路：直接检索复杂度过高，之前考虑过按对角线来排查的，但是在对角线上的元素不满足大小依次增长的条件，无法用类似BFS层级遍历的方法

- 二分搜索，该值的范围为`[1,N*M]`，使用中值`mid`搜索区间，并判断满足小于`mid`的值的个数`cnt`(依据每个元素的值为`x*y`确定该行有多少个值小于`mid`)
- 二分查找的判断条件：
  - `left < right`
  - `cnt<=N*M-K`：`mid`的值还较小，使`left = mid+1`
  - `else:right = mid` . 

- 循环跳出条件为`left == right`，区间左闭右开搜索。

```python
N,M,K = list(map(int,input().split()))
K = N*M - K

left,right = 1,N*M
while left < right:
    mid = (left+right)//2
    
    #小于mid的计数
    cnt = 0
    
    #直接通过M的值排除掉较小的一些行,这些行中最大元素都是乘M
    cnt += mid//M*M
    
    #遍历之后的行，通过行号计算该行中有多少值小于mid
    for row in range(mid//M+1,N+1):
        cnt += mid//row
    
    #通过cnt计数判断第k个的范围，这里的k已经是第k小
    if cnt <= K:
        left = mid + 1
    else:
        right = mid

print(left)
```

