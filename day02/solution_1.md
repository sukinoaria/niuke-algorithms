### 1. [迷宫游戏](<https://www.nowcoder.com/questionTerminal/c356fb7d1678419a9e9aa3c6f5a05765?answerType=1&f=discussion>)
来源：[小红书2020校招算法笔试题卷二](<https://www.nowcoder.com/test/23568060/summary>)

薯队长最近在玩一个迷宫探索类游戏，迷宫是一个N*N的矩阵形状，其中会有一些障碍物禁止通过。这个迷宫还有一个特殊的设计，它的左右 边界以及上下边界是连通的，比如在(2,n)的位置继续往右走一格可以到(2,1)，在(1,2)的位置继续往上走一格可以到(n,2)。请问薯队长从起点位置S，最少走多少格才能到达迷宫的出口位置E。 

```
输入描述:
第一行正整数N,接下来N行字符串
’.’表示可以通过
’#’表示障碍物
’S’表示起点（有且仅有一个）
’E’表示出口（有且仅有一个）
对于50%的数据N<10
对于100%的数据N<10^3 

输出描述:
输出一个整数。表示从S到E最短路径的长度,无法到达则输出-1 

示例1

输入
5
.#...
..#S.
.E### 
..... 
.....

输出
4
```

#### 分析

使用BFS从开始节点S向外围搜索，通过类似于树的层次级遍历的方法，使用队列`queue.deque`存储当前层的节点坐标，并逐个取出来再向外层扩展。**注意在添加新的节点到队列过程中要设定新节点为‘#’,不然在下一轮的搜索中这个节点会被重复搜索，从而导致在一些case上超时。**

```python
from queue import deque

def bfs(matrix, i, j, N):
    length = 0
    que = deque()
    que.append((i, j))
    while que:
        length += 1
        # 遍历当前层的所有节点
        for _ in range(len(que)):
            x, y = que.popleft()
            for dx, dy in [[-1, 0], [1, 0], [0, 1], [0, -1]]:
                new_x = (x + dx) % N
                new_y = (y + dy) % N
                if matrix[new_x][new_y] == 'E':
                    return length
                elif matrix[new_x][new_y] != '#':
                    #提前设定为障碍，避免重复访问
                    matrix[new_x][new_y] = '#'
                    que.append((new_x, new_y))
    return -1

def main():
    N = int(input())
    matrix = [[None for _ in range(N)] for _ in range(N)]
    for i in range(N):
        matrix[i] = list(input())

    for i in range(N):
        for j in range(N):
            if matrix[i][j] == 'S':
                return bfs(matrix, i, j, N)
    return -1
print(main())
```

