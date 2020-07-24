### [小A最多会新认识多少的人](<https://www.nowcoder.com/practice/1fe6c3136d2a45fa8ef555b459b6dd26?tpId=149&&tqId=33972&rp=1&ru=/ta/exam-bilibili&qru=/ta/exam-bilibili/question-ranking>)

小A参加了一个n人的活动，每个人都有一个唯一编号i(i>=0 & i<n)，其中m对相互认识，在活动中两个人可以通过互相都认识的一个人介绍认识。现在问活动结束后，小A最多会认识多少人？

```
输入描述:
第一行聚会的人数：n（n>=3 & n<10000）；
第二行小A的编号: ai（ai >= 0 & ai < n)；
第三互相认识的数目: m（m>=1 & m
< n(n-1)/2）；
第4到m+3行为互相认识的对，以','分割的编号。
输出描述:
输出小A最多会新认识的多少人？
示例1
输入
7
5
6
1,0
3,1
4,1
5,3
6,1
6,5
输出
3
```

#### 分析

- 通过`dict`存储图的边信息，每个`key`对应一个`list`
- 然后通过BFS遍历，通过`visited`标记是否访问过。

```python
#deque pop(0)速度要更快一点
from collections import deque

N = int(input())
cur_id = int(input())
M = int(input())

graph_link_dict = {}
for i in range(N):
    graph_link_dict[i] = []
for _ in range(M):
    node1,node2 = list(map(int,input().split(',')))
    graph_link_dict[node1].append(node2)
    graph_link_dict[node2].append(node1)

visited = [False]*N
new_set = set()

queue = deque()
for node in graph_link_dict[cur_id]:
    queue.append(node)
#BFS
while queue:
    node = queue.popleft()
    if visited[node]:
        continue
    for to_node in graph_link_dict[node]:
        if to_node != cur_id:
            queue.append(to_node)
    visited[node] = True
    new_set.add(node)
print(len(new_set)-len(graph_link_dict[cur_id]))
```

