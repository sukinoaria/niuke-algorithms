### [分贝壳](<https://www.nowcoder.com/practice/9b59014cc1544aeeb4082f5f37ecfaea?tpId=122&&tqId=33725&rp=1&ru=/ta/exam-wangyi&qru=/ta/exam-wangyi/question-ranking>)

牛牛和妞妞去海边捡了一大袋美丽的贝壳，千辛万苦地运回家后，牛牛和妞妞打算分掉这些贝壳。
牛牛提出，他和妞妞轮流从还没有分配的贝壳中取一定数量的贝壳，直到贝壳分完为止。分配规则是牛牛每次取剩余贝壳的1/10（向下取整），妞妞每次固定取m个贝壳，妞妞先取。
妞妞想要得到不少于一半的贝壳，又不想太过分，那么她一次最少取多少个贝壳才能得到不少于一半的贝壳呢？

```
输入描述:
一个正整数n，表示贝壳的总数量，1<=n<=1000000000000000000。
输出描述:
一个正整数m，表示妞妞一次最少取的贝壳数量。
示例1
输入
10
输出
1
示例2
输入
70
输出
3
```

#### 分析

通过一个函数来计算妞妞分到的个数，并用二分查找。

```python
from math import ceil

def check_num(N,m):
    x1,x2 = 0,0
    while N > 0:
        #lady first
        t2 = m if m <= N else N
        N -= t2
        x2 += t2
        
        t1 = N // 10
        N -= t1
        x1 += t1
    return x2

N = int(input())
left,right = 1,N
while left <= right :
    mid = (left+right)//2
    x2 = check_num(N, mid)
    if x2 > ceil(N/2):
        right = mid -1
    else:
        left = mid + 1
print(left)
```

