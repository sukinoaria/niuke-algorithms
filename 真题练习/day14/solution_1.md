### [目的地最短步数](https://www.nowcoder.com/practice/24ec35c2a8054a7b831a5a3ea660d729?tpId=146&&tqId=33970&rp=1&ru=/ta/exam-cmbxyk&qru=/ta/exam-cmbxyk/question-ranking)

牛牛手中有三根木棍,长度分别是a,b,c。牛牛可以把任一一根木棍长度削短,牛牛的目标是让这三根木棍构成一个三角形,并考虑你从家出发步行去往一处目的地，该目的地恰好离你整数单位步长（大于等于1）。你只能朝向该目的地或者背向该目的地行走，而你行走的必须为单位步长的整数倍，且要求你第N次行走必须走N步。
请就给出目的地离你距离，判断你是否可以在有限步内到达该目的地。如果可以到达的话，请计算到达目的地的最短总步数(不能到达则输出-1)。

```
输入描述:
1个整数：目的地离你距离T
输出描述:
1个整数：最短总步数（进行了多少次行走）
示例1
输入
2
输出
3
说明
距离目的地2， 需要3步：朝向走1，背向走2，朝向走3且牛牛还希望这个三角形的周长越大越好。
```

#### 分析

- 层次遍历，每次有加和减`i`两个选项，将其结果送到队列中。

- 使用层次遍历的原因：方便设定终止条件，如果当前层所有的位置和下一步的步数和都大于`N`的话，就再也不会走到指定的位置了。

```python
from collections import deque
N = int(input())

que = deque([(0,1)])
while que:
	# 标记当前层是不是还有小于N的值
    SMALLER = False
    for _ in range(len(que)):
        cur_pos,step = que.popleft()
        if cur_pos == N:
            print(step-1)
            exit()
        if cur_pos+ step <= N:
            SMALLER = True
        que.append([cur_pos+step,step+1])
        que.append([cur_pos-step,step+1])
    if not SMALLER:
        print(-1)
        break
```

