### [种花](<https://www.nowcoder.com/practice/09066b2c010f4218adb1a1db42dbb236?tpId=128&&tqId=33814&rp=1&ru=/ta/exam-meituan&qru=/ta/exam-meituan/question-ranking>)

题目给定a1,a2...an，这样一个长度为n的序列，现在你可以给其中一些元素加上一个值x（只能加一次），然后可以给另外一公园里有N个花园，初始时每个花园里都没有种花，园丁将花园从1到N编号并计划在编号为i的花园里恰好种A_i朵花，他每天会选择一个区间[L，R]（1≤L≤R≤N）并在编号为L到R的花园里各种一朵花，那么园丁至少要花多少天才能完成计划？

```
输入描述:
第一行包含一个整数N，1≤N≤10^5。

第二行包含N个空格隔开的整数A_1到A_N，0≤A_i≤10^4。
输出描述:
输出完成计划所需的最少天数。
示例1
输入
5
4 1 8 2 5
输出
14
```

#### 思路

- 贪心：相邻花圃需要的花朵数的差值是一定需要种植的，最后在额外加上循环中未计算的最后一个花圃的个数。

```python
n = int(input())
l = list(map(int, input().split()))
res = 0
for i in range(n-1):
    res += max(0, l[i] - l[i+1])
print(res + l[-1])
```

- 动态规划：`dp[i]`前i个编号的花圃满足条件所需要的天数，因此，只需要考虑`A[i]`和`A[i-1]`的大小，如果`A[i]<A[i-1]`，则不需要花费额外天数，否则需要额外花费其差的天数`abs(A[i]-a[i-1])`。
- `dp[0]=A[0]`

```python

N = int(input())
nums = list(map(int, input().split()))

dp = [0 for _ in range(N)]
dp[0] = nums[0]

for i in range(1,N):
    if nums[i] <= nums[i-1]:
        dp[i] = dp[i-1]
    else:
        dp[i] = dp[i-1] + nums[i]-nums[i-1]
print(dp[-1])
```

