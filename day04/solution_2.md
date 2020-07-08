### [子数组查找](<https://www.nowcoder.com/questionTerminal/4406e29ed847446e9745d75f43fad3fe>)

来源：[深信服校园招聘算法练习卷](<https://www.nowcoder.com/test/23358504/summary>)

给定长度为N的整数数组，以及M个互不相同的整数，请找出包含这M个整数的最短子数组。

例如：给定数组[4 2 1 3]，包含数字集{2, 3}的最短子数组是[2 1 3]，包含数字集{1, 3}的最短子数组是[1 3]。

```
输入描述:
第一行一个正整数T（T<=10），表示T个测试样例；
对于每个测试样例，
输入正整数N（N<=100,000），表示数组长度；
接下来输入N个正整数，所有整数都>=0且<=1,000,000,000；
输入正整数M（M<=N），表示M个互不相同的整数；
接下来输入M个整数，表示要查询的整数，已保证互不相同。

有部分测试样例满足N<=1,000。

输出描述:
输出T行，每行一个正整数，表示最短子数组的长度。如果不存在，输出0
示例1
输入
1
4
4 2 1 3
2
2 3
输出
3
```

#### 思路

- 使用滑动窗口来匹配子串，分别用`start`和`end`两个变量记录位置，然后通过字典记录需要的字符串的个数，`key`为需要的字符，`val`为个数，额外使用一个计数变量`satisfied`记录满足匹配条件的字符个数，当其值等于要查找的子串长度时说明找到了满足条件的子串。
  - 开始时一直移动`end`并检查是否是需要的字符并计数，当数量满足时开始移动左边界`start`从而缩小范围，直到`end`遍历到数组的最后。

```python
def find_min_length(M,N,m_nums,need_dict):
    min_length = 100000
    satisfied = 0
    #存储目标字符串中需要的字符的个数
    src_dict = {}
    start,end = 0,0
    #滑动窗口最后的位置，end到达数组尾
    while end < M:
        # end向右滑动知道找到包含need所有字符的窗口
        if m_nums[end] in need_dict.keys():
            src_dict[m_nums[end]] = src_dict.get(m_nums[end],0)+1
        if src_dict[m_nums[end]] == need_dict[m_nums[end]]:
            satisfied += 1
        # 找到满足条件的子串后求其长度，并移动左边的窗口坐标
        while satisfied == N:
            min_length = min(min_length,end-start+1)
            if m_nums[start] in need_dict.keys():
                src_dict[m_nums[start]] -= 1
                # 重新判断新的窗口是否符合条件，不符合条件的话需要移动右窗口
                if src_dict[m_nums[start]] < need_dict[m_nums[start]]:
                    satisfied -= 1
            start += 1
        end += 1
    return min_length if min_length != 100000 else 0
     
def main():
    T = int(input())
    for i in range(T):
        M = int(input())
        m_nums = list(map(int,input().split()))
        N = int(input())
        n_nums = list(map(int,input().split()))
        
        need_dict = {}
        for i in range(N):
            need_dict[n_nums[i]] = need_dict.get(n_nums[i],0)+1
        min_length = find_min_length(M,N,m_nums, need_dict)
        print(min_length)
main()
```

