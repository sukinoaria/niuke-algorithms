### [最大间隔](<https://www.nowcoder.com/practice/3a571cdc72264d76820396770a151f90?tpId=155&&tqId=34000&rp=1&ru=/ta/exam-mogujie&qru=/ta/exam-mogujie/question-ranking>)

给定一个递增序列，a1 <a2 <...<an 。定义这个序列的最大间隔为$d=max\{a_{i+1} - a_i \}(1≤i<n)$,现在要从a2 ,a3 ..an-1 中删除一个元素。问剩余序列的最大间隔最小是多少？

```
输入描述:
第一行，一个正整数n(1<=n<=100),序列长度;接下来n个小于1000的正整数，表示一个递增序列。
输出描述:
输出答案。
示例1
输入
5
1 2 3 7 8
输出
4
```

#### 分析

- 只要元素个数大于三，删除某个值其最大间隔不会发生改变。

```python
while True:
    try:
        N = int(input())
        nums = list(map(int,input().split()))

        max_inter = -1
        for i in range(1,N):
            max_inter = max(max_inter,nums[i]-nums[i-1])

        if N == 3:
            print(nums[2]-nums[0])
        else:
            print(max_inter)
    except:
        break
```

