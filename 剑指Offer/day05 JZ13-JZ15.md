## day 05

### JZ13. 调整数组顺序使奇数位于偶数前面
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

#### 分析

- 用空间换时间，使用两个数组存奇数和偶数，最后合并

- 如果不要求相对位置不变的话，可以用一前一后的双指针，前面指向偶数、后面奇数时进行交换。
- `Python - filter`用于过滤序列。`filter(function,iterable)`

```python
# -*- coding:utf-8 -*-
class Solution:
    def reOrderArray(self, array):
        # write code here
        o = filter(lambda x:x%2!=0,array)
        e = filter(lambda x:x%2==0,array)
        return o + e
```

### JZ14. 链表中倒数第k个节点
输入一个链表，输出该链表中倒数第k个结点。

#### 分析

坑点：

- 注意例外情况
  - k大于链表长度
  - k = 0

```python
class Solution:
    def FindKthToTail(self, head, k):
        # write code here
        if not head or k < 1:return None
        root = head
        while k :
            k -= 1
            if root:
                root = root.next
            else:
                return None
        while root:
            head = head.next
            root = root.next
        return head
```

### JZ15.反转链表

输入一个链表，反转链表后，输出新链表的表头。

#### 分析

使用头插入法进行遍历插入到新的表头结点之后，最后返回表头结点后面的节点。

```python
class Solution:
    # 返回ListNode
    def ReverseList(self, pHead):
        # write code here
        n_head = ListNode(0)
        while pHead:
            nex = pHead.next
            pHead.next = n_head.next
            n_head.next = pHead
            pHead = nex
        return n_head.next
```

