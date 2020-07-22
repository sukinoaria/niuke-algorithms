### [平方串](<https://www.nowcoder.com/practice/b43fb39898f448e39adbcffde5ff0dfc?tpId=140&&tqId=33924&rp=1&ru=/ta/exam-iqiyi&qru=/ta/exam-iqiyi/question-ranking>)

如果一个字符串S是由两个字符串T连接而成,即S = T + T, 我们就称S叫做平方串,例如"","aabaab","xxxx"都是平方串. 牛牛现在有一个字符串s,请你帮助牛牛从s中移除尽量少的字符,让剩下的字符串是一个平方串。换句话说,就是找出s的最长子序列并且这个子序列构成一个平方串。

```
输入描述:
输入一个字符串s,字符串长度length(1 ≤ length ≤ 50),字符串只包括小写字符。
输出描述:
输出一个正整数,即满足要求的平方串的长度。
示例1
输入
frankfurt
输出
4
```

#### 分析

先从[1,N-2]切分原字符串为两个字符串`s`和`t`，再求他们的最长公共子序列。

- 状态转移：

```python
dp[i][j]  #i为字符串s的遍历索引，j为t的索引

#当 s[i-1] == t[j-1]时，dp[i][j] = [i-1][j-1]+1

#不相等时，转移的路径分别有三个：
dp[i-1][j-1] :  #即i与j进行对齐
dp[i-1][j]   :  #即i-1与j进行对齐
dp[i][j-1]   :  #即i与j-1进行对齐
```

- 注意索引开始遍历的值以及比较的位置。

```python
def calc_LCS(s,t):
    dp = [[0] * (len(t)+1) for _ in range(len(s)+1)]
    for i in range(1,len(s)+1):
        for j in range(1,len(t)+1):
            if s[i-1] == t[j-1]:
                dp[i][j] = dp[i-1][j-1]+1
            else:
                dp[i][j] = max(dp[i-1][j-1],dp[i-1][j],dp[i][j-1])
    return dp[-1][-1]

s = input()

max_length = 0
for i in range(1,len(s)-1):
    max_length = max(max_length,calc_LCS(s[:i],s[i:]))
print(max_length*2)
```

