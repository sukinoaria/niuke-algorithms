## day 06

### JZ16. 合并排序链表
输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

```python
class Solution:
    # 返回合并后列表
    def Merge(self, pHead1, pHead2):
        # write code here
        res = head = ListNode(0)
        while pHead1 and pHead2:
            if pHead1.val < pHead2.val:
                head.next = pHead1
                pHead1 = pHead1.next
            else:
                head.next = pHead2
                pHead2 = pHead2.next
            head = head.next
        head.next = pHead1 if pHead1 else pHead2
        return res.next
```

### JZ17. 树的子结构
输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

#### 分析

- 从根节点开始判断，如果其中有一个为空，则不是
- 否则，分三种情况：
  - 即从根节点开始A和B就有同样的结构，那么需要比较A和B的值以及其左右子树是不是相同
  - A的left子树和B结构相同
  - A的right子树和B结构相同
- 三种情况满足其一即可。

```python
class Solution:
    def HasSubtree(self, pRoot1, pRoot2):
        # write code here
        if not pRoot1 or not pRoot2:return False
        return self.helper(pRoot1,pRoot2) or self.HasSubtree(pRoot1.left, pRoot2) or self.HasSubtree(pRoot1.right, pRoot2)
        
    def helper(self,root1,root2):
        if not root2:return True
        if not root1:return False
        return root1.val == root2.val and self.helper(root1.left,root2.left) and self.helper(root1.right,root2.right)
```

### JZ18.二叉树的镜像

操作给定的二叉树，将其变换为源二叉树的镜像。

#### 分析

递归翻转所有的子树

```python
class Solution:
    # 返回镜像树的根节点
    def Mirror(self, root):
        # write code here
        def helper(root):
            if not root:return None
            root.left,root.right = root.right,root.left
            helper(root.left)
            helper(root.right)
            return root
        return helper(root)
```

