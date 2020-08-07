### [拼凑三角形](<https://www.nowcoder.com/practice/d9f5dbd3b57d450e8406e102573d4bdd?tpId=140&&tqId=33914&rp=1&ru=/ta/exam-iqiyi&qru=/ta/exam-iqiyi/question-ranking>)

牛牛手中有三根木棍,长度分别是a,b,c。牛牛可以把任一一根木棍长度削短,牛牛的目标是让这三根木棍构成一个三角形,并且牛牛还希望这个三角形的周长越大越好。

```
输入描述:
输入包括一行,一行中有正整数a, b, c(1 ≤ a, b, c ≤ 100), 以空格分割
输出描述:
输出一个整数,表示能拼凑出的周长最大的三角形。
示例1
输入
1 2 3
输出
5
```

#### 分析

**把任一一根木棍长度削短**，穷举，计算出所有的可能性选最大的。

如果可以随意削短多根的话，可以使用BFS。

```python
from collections import deque

def is_triangle(a,b,c):
    if a+b>c and a+c>b and b+c>a:
        return True
    return False

def calc_max_length(a,b,c):
    for i in range(a):
        if is_triangle(a-i, b, c):
            return a+b+c-i
    return 0

a,b,c = list(map(int,input().split()))
max_length = max(calc_max_length(a, b, c),calc_max_length(b, a, c),calc_max_length(c,a, b))
print(max_length)
```

