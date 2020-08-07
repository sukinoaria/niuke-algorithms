### [漂流船](<https://www.nowcoder.com/practice/0e6cb06ec63148ed952f887a787f0103?tpId=146&&tqId=33968&rp=1&ru=/ta/exam-cmbxyk&qru=/ta/exam-cmbxyk/question-ranking>)

公司组织团建活动，到某漂流圣地漂流，现有如下情况：
员工各自体重不一，第 i 个人的体重为 people[i]，每艘漂流船可以承载的最大重量为 limit。
每艘船最多可同时载两人，但条件是这些人的重量之和最多为 limit。
为节省开支，麻烦帮忙计算出载到每一个人所需的最小船只数(保证每个人都能被船载)。

```
输入描述:
第一行输入参与漂流的人员对应的体重数组，

第二行输入漂流船承载的最大重量
输出描述:
所需最小船只数
示例1
输入
1 2
3
输出
1
```

#### 分析

- 简单题，贪心：先排序然后使用`left`和`right`指针向中间搜索
  - 如果`left==right`,只剩下一个人，`count+1`
  - 如果和小于等于`limit`，两个指针向中间移动，`count+1`
  - 否则，right位置的人超重了，单人一个船，`count+1`

```python
nums = list(map(int,input().split()))
limit = int(input())

count = 0
nums = sorted(nums)
left,right = 0,len(nums)-1
while left <= right:
    if left == right :
        count += 1
        break
    elif nums[left]+nums[right]<=limit:
        left += 1
        right -= 1
    else:
        right -= 1
    count += 1
print(count)
```

