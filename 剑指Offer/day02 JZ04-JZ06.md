## day 02

### JZ4. 重建二叉树
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

#### 分析

根据先序遍历的结果，其第一个节点为子树的根节点，然后找到其在中序遍历中的位置可以将剩下的节点划分到左右子树范围内，然后再递归构建其子树。

- 使用dict存储中序遍历的结果，可以节约反复查找先序遍历第一个节点在中序遍历中的位置。

- 需要注意的点是在查找到中序遍历的位置时确定好左右子树结点的范围
  - pre数组索引：`[pre_left,pre_right]`,tin数组索引：`[tin_left,tin_right]`
  - 对找到的中序遍历划分索引`inorder_idx`,其左子树节点个数为`inorder_idx-tin_left`
  - 根据节点个数对pre数组进行划分：pre数组第一个节点为根节点，左子树从`pre_left+1`开始：`[pre_left+1:pre_left+inorder_idx-tin_left+1]`,右子树为`[pre_left+inorder_idx-tin_left+1:pre_right]`
  - 对tin数组进行划分：左子树：`[tin_left,inorder_idx]`，右子树不包含`inorder`节点：`[inorder_idx+1:tin_right]`

```python
from collections import defaultdict
class Solution:
    # 返回构造的TreeNode根节点
    def reConstructBinaryTree(self, pre, tin):
        # write code here
        inorder_dict = defaultdict(int)
        for i in range(len(tin)):
            inorder_dict[tin[i]] = i
        
        def helper(pre_left,pre_right,t_left,t_right):
            if pre_left>=pre_right:
                return None
            root_node = pre[pre_left]
            inorder_idx = inorder_dict[root_node]
            root = TreeNode(root_node)
            root.left  = helper(pre_left+1,pre_left+inorder_idx-t_left+1,t_left,inorder_idx)
            root.right = helper(pre_left+inorder_idx-t_left+1,pre_right,inorder_idx+1,t_right)
            return root
        return helper(0,len(pre),0,len(pre))
```

### JZ5. 用两个栈实现队列
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

#### 分析

双栈实现队列的大致思路：

- 每次插入元素时放入stack1,此时stack1的元素都是反向的。
- 需要弹出元素时，判断stack2是否为空：
  - stack2不为空，则弹出栈顶元素
  - 否则，将stack1中的所有元素弹出，并压入stack2中，此时在stack2中最上面为最先插入的元素

```c++
class Solution
{
public:
    void push(int node) {
        stack1.push(node);
    }
    int pop() {
        if (stack2.empty())
        {
            while(!stack1.empty())
            {
                stack2.push(stack1.top());
                stack1.pop();
            }
        }
        int node = stack2.top();
        stack2.pop();
        return node;
    }
private:
    stack<int> stack1;
    stack<int> stack2;
};
```

### JZ6. 旋转数组的最小数字

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。

```
例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。
```

#### 分析

可以看出，该旋转数组是由两个非递减序列构成的，**且在大多数条件下满足第一个元素大于等于最后一个元素**，可以根据这个性质通过变形的二分查找来找出两个序列中的最小值(**即第二个序列的第一个值**)当作最小元素的开始位置：

- 已知左右边界`left`和`right`，取其中间值`mid`并判断：
  - 如果mid处的元素大于等于left处的元素，则说明mid位于第一个序列中，移动left到mid
  - 如果mid处的元素小于等于right处的元素，则说明mid位于第二个序列中，移动right到mid
  - 循环条件：`val[left]>=val[right]`
  - 终止条件：满足循环条件且`right-left=1`时，即left是最后一个元素，right为第二个序列的第一个元素，返回right
  - 例外情况：如果比较时`val[left]==val[mid]==val[right]`，则无法确定(`[1,0,1,1,1]`)，此时需要改用顺序查找。

```python
# -*- coding:utf-8 -*-
class Solution:
    def minNumberInRotateArray(self, rotateArray):
        # write code here
        def get_min_index(rotateArray,left,right):
            min_idx = left
            for i in range(left+1,right):
                if rotateArray[i] < rotateArray[min_idx]:
                    min_idx = i
            return min_idx
        
        if not rotateArray:return 0
        min_index = 0
        left,right = 0,len(rotateArray)-1
        while rotateArray[left] >= rotateArray[right]:
            if right - left == 1:
                min_index = right
                break
            mid = (left+right)//2
            if rotateArray[mid] == rotateArray[left] and rotateArray[mid] == rotateArray[right]:
                min_index = get_min_index(rotateArray,left,right)
                break
            elif rotateArray[mid] >= rotateArray[left]:
                left = mid
            elif rotateArray[mid] <= rotateArray[right]:
                right = mid
        return rotateArray[min_index]

```

