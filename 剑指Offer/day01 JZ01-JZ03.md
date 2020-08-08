## day 01

### JZ1. 二叉树组中的查找
在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

```
1 2 3
2 3 4
6 7 8
```

**分析**：从左上角开始遍历，`target`大于该值后就像下遍历，否则向左遍历，直到找到对应的值或者到达边界。

```python
# -*- coding:utf-8 -*-
class Solution:
    # array 二维列表
    def Find(self, target, array):
        # write code here
        M,N = len(array),len(array[0])
        i,j = 0,N-1
        while i < M and j >= 0:
            if array[i][j] == target:
                return True
            elif array[i][j] < target:
                i+=1
            else:
                j-=1
        return False
```

### JZ2. 替换空格
请实现一个函数，将一个字符串中的每个空格替换成“`%20`”。例如，当字符串为`We Are Happy`.则经过替换之后的字符串`为We%20Are%20Happy`。

```python
# -*- coding:utf-8 -*-
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        return "%20".join(s.split(" "))
```

取巧了，回头写一遍C++的

### JZ3. 从尾到头打印链表

输入一个链表，按链表从尾到头的顺序返回一个`ArrayList`。

**递归版的**

```python
# -*- coding:utf-8 -*-
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # 返回从尾部到头部的列表值序列，例如[1,2,3]
    def printListFromTailToHead(self, listNode):
        # write code here
        res = []
        def helper(node):
            if not node:
                return
            helper(node.next)
            res.append(node.val)
        helper(listNode)
        return res
```

