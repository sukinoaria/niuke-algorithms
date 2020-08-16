## day 07

### JZ19. 顺时针打印矩阵
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵：

```
 1 2 3 4
 5 6 7 8
 9 10 11 12
 13 14 15 16
```

 则依次打印出数字

```
1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.
```

- 思路一：基于Python的trick：每次取一行后旋转矩阵

```python
#zip函数示例
a = [[1,2,3],[4,5,6]]

b = list(zip(*a))[::-1]
#b: [(3, 6), (2, 5), (1, 4)]
```

```python
# -*- coding:utf-8 -*-
class Solution:
    # matrix类型为二维列表，需要返回列表
    def printMatrix(self, matrix):
        # write code here
        res = []
        while len(matrix):
            res.extend(matrix.pop(0))
            matrix = list(zip(*matrix))[::-1]
        return res
```

- 思路二 ： 不使用zip，而是基于list的pop来做
  - 先弹出第一行，然后遍历最后一列，再弹出最后一行，之后遍历第一列。

```python
# -*- coding:utf-8 -*-
class Solution:
    # matrix类型为二维列表，需要返回列表
    def printMatrix(self, matrix):
        # write code here
        res = []
        while matrix:
            res.extend(matrix.pop(0))
            if matrix and matrix[0]:
                for row in matrix:
                    res.append(row.pop())
            if matrix and matrix[0]:
                res.extend(matrix.pop()[::-1])
            if matrix and matrix[0]:
                for row in matrix[::-1]:
                    res.append(row.pop(0))
        return res
```

### JZ20. 包含min函数的栈

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

#### 分析

- 使用一个额外的辅助栈来存储最小值，当原本的最小值弹出时可以以O(1)复杂度找到次小的值。

```python
# -*- coding:utf-8 -*-
class Solution:
    def __init__(self):
        self.stack = []
        self.min_stack = [1e9]
    def push(self, node):
        self.stack.append(node)
        if node < self.min_stack[-1]:
            self.min_stack.append(node)
    def pop(self):
        node = self.stack.pop()
        if node == self.min_stack[-1]:
            self.min_stack.pop()
        return node
    def top(self):
        return self.stack[-1]
    def min(self):
        return self.min_stack[-1]
```

### JZ21.栈的压入、弹出序列

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

#### 分析

- 使用辅助栈进行模拟

- 对出栈序列的每一个值，
  - 如果该值在栈顶上，则弹出
  - 否则，根据入栈序列一次入栈直到遇到该数值
- 最后出栈序列遍历完成但没有找到对应元素则不是合法序列。

```python
# -*- coding:utf-8 -*-
class Solution:
    def IsPopOrder(self, pushV, popV):
        # write code here
        stack = []
        idx = 0
        for val in popV:
            if not stack or stack[-1] != val:
                # 在入栈序列中找到val元素，如果遍历完也找不到 说明不合法
                while idx < len(pushV) and pushV[idx] != val:
                    stack.append(pushV[idx])
                    idx += 1
                if idx >= len(pushV):
                    return False
                idx += 1
            else:
                stack.pop()
        if not stack: return True
        return False
```

