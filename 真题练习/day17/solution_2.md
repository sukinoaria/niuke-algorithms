### [马戏团](<https://www.nowcoder.com/practice/c2afcd7353f84690bb73aa6123548770?tpId=170&&tqId=34060&rp=1&ru=/ta/exam-sohu&qru=/ta/exam-sohu/question-ranking>)

搜狐员工小王最近利用假期在外地旅游，在某个小镇碰到一个马戏团表演，精彩的表演结束后发现团长正和大伙在帐篷前激烈讨论，小王打听了下了解到， 马戏团正打算出一个新节目“最高罗汉塔”，即马戏团员叠罗汉表演。考虑到安全因素，要求叠罗汉过程中，站在某个人肩上的人应该既比自己矮又比自己瘦，或相等。 团长想要本次节目中的罗汉塔叠的最高，由于人数众多，正在头疼如何安排人员的问题。小王觉得这个问题很简单，于是统计了参与最高罗汉塔表演的所有团员的身高体重，并且很快找到叠最高罗汉塔的人员序列。 现在你手上也拿到了这样一份身高体重表，请找出可以叠出的最高罗汉塔的高度，这份表中马戏团员依次编号为1到N。

```
输入描述:
首先一个正整数N，表示人员个数。 
之后N行，每行三个数，分别对应马戏团员编号，体重和身高。
输出描述:
正整数m，表示罗汉塔的高度。
示例1
输入
6
1 65 100
2 75 80
3 80 100
4 60 95
5 82 101
6 81 70
输出
4
```

#### 分析

- 动态规划，求排好序的最长上升子序列

```python
while True:
    try:
        N = int(input())
        nums = []
        for _ in range(N):
            _,weight,height = list(map(int,input().split()))
            nums.append([weight,height])
        nums.sort(key = lambda x:x[1])
        nums.sort(key = lambda x:-x[0])
        max_num = 0
        dp = [1]*N
        for i in range(1,N):
            for j in range(i):
                if nums[i][1] <= nums[j][1]:
                    dp[i] = max(dp[i],dp[j]+1)

            max_num = max(max_num,dp[i])
        print(max_num)
    except:
        break
```

