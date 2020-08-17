## day 08

### JZ22. 从上往下打印二叉树
从上往下打印出二叉树的每个节点，同层节点从左至右打印。

```python
class Solution:
    # 返回从上到下每个节点值列表，例：[1,2,3]
    def PrintFromTopToBottom(self, root):
        # write code here
        if not root:return []
        que = [root]
        res = []
        while que:
            node = que.pop(0)
            res.append(node.val)
            if node.left:que.append(node.left)
            if node.right:que.append(node.right)
        return res
```

### JZ23. 二叉搜索树的后序遍历序列

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则返回true,否则返回false。假设输入的数组的任意两个数字都互不相同。

#### 分析

- 结合二叉搜索树和后序遍历的性质，选取最后一个元素pivot，然后遍历找到一个分界点i，i之前的都小于pivot，之后的都大于pivot，递归比较两个子树是否满足条件。

```python
# -*- coding:utf-8 -*-
class Solution:
    def VerifySquenceOfBST(self, sequence):
        # write code here
        if not sequence:return False
        pivot = sequence[-1]
        for i in range(len(sequence)):
            if sequence[i] > pivot:
                break
        for j in range(i+1,len(sequence)):
            if sequence[j] < pivot:
                return False
        if i > 0:
            left = self.VerifySquenceOfBST(sequence[:i])
        else:
            left = True
        if i < len(sequence)-1:
            right = self.VerifySquenceOfBST(sequence[i:-1])
        else:
            right = True
        return left and right
```

### JZ24.二叉树中和为某一值的路径

输入一颗二叉树的根节点和一个整数，按字典序打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

#### 分析

- 只在叶子节点上有结果，递归，终止条件为：叶子节点且值等于target


```python
class Solution:
    # 返回二维列表，内部每个列表表示找到的路径
    def FindPath(self, root, expectNumber):
        # write code here
        if not root:return []
        res = []
        path = []
        def helper(node,target):
            if not node:return
            if not node.left and not node.right and node.val == target:
                res.append(list(path)+[node.val])
            if node.left or node.right:
                target -= node.val
                path.append(node.val)
                if node.left:
                    helper(node.left,target)
                if node.right:
                    helper(node.right,target)
                target += node.val
                path.pop()
            
        helper(root,expectNumber)
        return res
```

