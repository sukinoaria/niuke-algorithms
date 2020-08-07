### [迷宫](<https://www.nowcoder.com/practice/6171d3a8748248248c21a3c8f330396d?tpId=149&&tqId=33976&rp=1&ru=/ta/exam-bilibili&qru=/ta/exam-bilibili/question-ranking>)

猛兽侠中精灵鼠在利剑飞船的追逐下逃到一个n*n的建筑群中，精灵鼠从（0,0）的位置进入建筑群，建筑群的出口位置为（n-1,n-1），建筑群的每个位置都有阻碍，每个位置上都会相当于给了精灵鼠一个固定值减速，因为精灵鼠正在逃命所以不能回头只能向前或者向下逃跑，现在问精灵鼠最少在减速多少的情况下逃出迷宫？

```
输入描述:
第一行迷宫的大小: n >=2 & n <= 10000；
第2到n+1行，每行输入为以','分割的该位置的减速,减速f >=1 & f < 10。
输出描述:
精灵鼠从入口到出口的最少减少速度？
示例1
输入
3
5,5,7
6,7,8
2,2,4
输出
19
```

#### 分析

即求到达`[N-1,N-1]`位置的最小和，动态规划(尝试了带memo的递归并不能AC)

- 初始条件：`dp[0,0]`位置的值即为`matrix[0][0]`，接下来先对第一行和第一列的结果进行计算(转移方式固定)
- 之后`dp[i][j] = min(dp[i-1][j],dp[i][j-1])+matrix[i][j]`

```python

N = int(input())
matrix = [[0]*N for _ in range(N)]
for i in range(N):
    matrix[i] = list(map(int,input().split(',')))

# 行和列值初始化
for i in range(1,N):
    matrix[0][i] += matrix[0][i-1]
    matrix[i][0] += matrix[i-1][0]

for i in range(1,N):
    for j in range(1,N):
        matrix[i][j] = min(matrix[i-1][j],matrix[i][j-1])+matrix[i][j]

print(matrix[-1][-1])
```

