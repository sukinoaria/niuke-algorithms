### [判断满二叉树是否是二叉搜索树](<https://www.nowcoder.com/practice/76fb9757332c467d933418f4adf5c73d?tpId=131&&tqId=33853&rp=1&ru=/ta/exam-kuaishou&qru=/ta/exam-kuaishou/question-ranking>)
题目描述
给定一棵满二叉树，判定该树是否为二叉搜索树，是的话打印True，不是的话打印False

说明：
a. 二叉搜索树（Binary Search Tree），它或者是一棵空树，或者是具有下列性质的二叉树： 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值； 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值； 它的左、右子树也分别为二叉搜索树。
b. 满二叉树，除最后一层无任何子节点外，每一层上的所有结点都有两个子结点二叉树
c. 树内节点数不超过 10000，非空节点值为大于0小于65536的整数，空树或空节点输入为None

```
输入描述:
从根节点开始，逐层输入每个节点的值，空树或空节点输入为None
比如：10,5,15,3,7,13,18
输出描述:
是二叉搜索树的话打印True，不是的话打印False
示例1
输入
10,5,15,3,7,13,18
输出
True
```

### 分析

先根据数组构建树，之后再中序遍历，判断是不是递增序列。

```python

class treeNode:
    def __init__(self,val):
        self.val = val
        self.left = None
        self.right = None

def build_tree(nums,index):
    if index >= len(nums) or nums[index] =="None":
        return None
    node = treeNode(int(nums[index]))
    node.left = build_tree(nums, index*2+1)
    node.right = build_tree(nums, index*2+2)
    return node

inorder_nums = []
def inorder(root):
    if not root:return
    inorder(root.left)
    inorder_nums.append(root.val)
    inorder(root.right)

nums = list(input().split(','))

if len(nums) <= 1:
    print("True")
    exit()

tree = build_tree(nums,0)
inorder(tree)

for i in range(len(inorder_nums)-1):
    if inorder_nums[i]>inorder_nums[i+1]:
        print("False")
        exit()
print("True")
```

