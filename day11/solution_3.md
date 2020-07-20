### [整数无序数组求第K大数](<https://www.nowcoder.com/practice/097ab63cffa847d89716f2ca8c23524f?tpId=152&&tqId=33991&rp=1&ru=/ta/exam-didi&qru=/ta/exam-didi/question-ranking>)

给定无序整数序列，求其中第K大的数，例如{45，67，33，21}，第2大数为45

```
输入描述:
输入第一行为整数序列，数字用空格分隔，如：45 67 33 21
输入第二行一个整数K，K在数组长度范围内，如：2
输出描述:
输出第K大的数，本例为第2大数：45
示例1
输入
45 67 33 21
2
输出
45
```

#### 分析

大根堆存储，之后取出K个数。

`heapq`为小根堆，加负号处理。

```python
from heapq import heapify,heappush,heappop

nums = list(map(lambda x :-int(x),input().split()))
K = int(input())

heapify(nums)

while K > 1:
    heappop(nums)
    K -= 1
print(-heappop(nums))
```

