### [相等序列](<https://www.nowcoder.com/practice/7492dceb022a4bbebb990695c107823e?tpId=122&&tqId=33723&rp=1&ru=/ta/exam-wangyi&qru=/ta/exam-wangyi/question-ranking>)

题目给定a1,a2...an，这样一个长度为n的序列，现在你可以给其中一些元素加上一个值x（只能加一次），然后可以给另外一些值减上一个值x（只能减一次），剩下的元素不能再进行操作。问最后有没有可能找到一个值x使所有元素的值相等。

```
输入描述:
输入第一行为一个整数k，代表有k个序列(k<100)，接下来有2*k行:
偶数行为一个整数n，代表给定序列的长度(1<=n<=100,000)
奇数行包含n个元素，a1,a2...an，代表序列中的元素(0<=ai<=100,000)

输出描述:
输出k行，每行一个YES或者NO
示例1
输入
1
5
1 3 3 2 1
输出
YES
```

#### 分析

根据题目的要求，对每个值只能进行**一次**加、减或不更改的操作，所以如果数组中`unique`的值大于等于4时一定不满足条件，小于等于2时一定满足条件，等于三时再比较三个书中是否存在一个数，使得另外两个数减去它的绝对值相等。

```python

def check_valid(N,nums):
    unique_values = set(nums)
    if len(unique_values) < 3:return "YES"
    elif len(unique_values) >= 4:return "NO"
    for val1 in unique_values:
        abs_minus_vals = set()
        for val2 in unique_values - set([val1]):
            abs_minus_vals.add(abs(val1-val2))
            if len(abs_minus_vals) > 1:
                break
        if len(abs_minus_vals) == 1:
            return "YES"
    return "NO"

T = int(input())
for t in range(T):
    N = int(input())
    nums = list(map(int,input().split()))
    print(check_valid(N,nums))
```

