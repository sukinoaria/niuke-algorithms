### [多多的电子字典](<https://www.nowcoder.com/questionTerminal/061d419c7cea4c658ee0484654b11c3e>)

来源：[拼多多2020校招部分编程题合集](<https://www.nowcoder.com/test/23354036/summary>)

多多鸡打算造一本自己的电子字典，里面的所有单词都只由a和b组成。
 每个单词的组成里a的数量不能超过N个且b的数量不能超过M个。
 多多鸡的幸运数字是K，它打算把所有满足条件的单词里的字典序第K小的单词找出来，作为字典的封面。  

```
输入描述:
共一行，三个整数N, M, K。(0 < N, M < 50, 0 < K < 1,000,000,000,000,000)

输出描述:
共一行，为字典序第K小的单词。
示例1
输入
2 1 4
输出
ab
说明
满足条件的单词里，按照字典序从小到大排列的结果是
a
aa
aab
ab
aba
b
ba
baa

备注:
对于40%的数据：0 < K < 100,000
对于100%的数据：0 < K < 1,000,000,000,000,000
题目保证第K小的单词一定存在
```

#### 分析

由不同的前缀`a`和`b`构成了两个子树，找第k个元素实际上就是先序遍历的过程，通过求子树中的唯一字符串个数可以快速地跳过一些无关的子树。

直接先序遍历往往会有过大的时间复杂度，可以通过带备忘录的递归算法求解出f(n,m)的值，从而避免大量的重复运算。

Base case:只有m或n不为零，则直接返回对应的值。

![](https://wx3.sinaimg.cn/large/006dXJzOly1ggl05ern6oj30rm0bn7wh.jpg)

```

# 计算包含N个a和M个b的子字典树包含的unique字符串的个数，从而和K进行
# 比较，以便选择跳过该子树或者进入该子树
count_dict = {}
def calc_subtree_str_num(N,M):
    if (N,M) in count_dict.keys():
        return count_dict[(N,M)]
    elif N == 0:
        count_dict[(N,M)] = M
    elif M == 0:
        count_dict[(N,M)] = N
    else:
        #分别以a和b得到的两个子树的个数统计加上a和b这两个节点
        count_dict[(N,M)] = calc_subtree_str_num(N-1,M) + calc_subtree_str_num(N,M-1) + 2
    return count_dict[(N,M)]

def main():
    N,M,K = list(map(int,input().split()))
    
    res = ""
    #当K=0时就找到了对应的字符串
    while K > 0:
        # 一般情况 N 和 M 都存在
        if N > 0 and M > 0:
            #获取当前情况下左子树的字符串个数，如果大于K说明结果在右子树
            left_str_cnt = calc_subtree_str_num(N-1, M)+1
            if K <= left_str_cnt:
                # 说明第k个在a子树下，添加字符'a'，并继续循环向下判断
                res += 'a'
                K -= 1 
                N -= 1
            else:
                # 在右子树下，K可以跳过left_str_cnt+1个值，1为左子树根节点'a'，配合上前缀也是一个unique的str
                res += 'b'
                K -= (left_str_cnt + 1)
                M -= 1
        #其他情况，N=0或者M=0时只需要一直添加字符即可,因为题上的说明不用考虑不存在
        elif N == 0 and M > 0:
            res += 'b'
            K -= 1
            M -= 1
        elif M == 0 and N > 0:
            res += 'a'
            K -= 1
            N -= 1
    return res
    
print(main())
```

