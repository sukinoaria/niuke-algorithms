### [分田地](<https://www.nowcoder.com/practice/fe30a13b5fb84b339cb6cb3f70dca699?tpId=182&&tqId=34283&rp=1&ru=/ta/exam-all&qru=/ta/exam-all/question-ranking>)

牛牛和 15 个朋友来玩打土豪分田地的游戏，牛牛决定让你来分田地，地主的田地可以看成是一个矩形，每个位置有一个价值。分割田地的方法是横竖各切三刀，分成 16 份，作为领导干部，牛牛总是会选择其中总价值最小的一份田地， 作为牛牛最好的朋友，你希望牛牛取得的田地的价值和尽可能大，你知道这个值最大可以是多少吗？

```
输入描述:
每个输入包含 1 个测试用例。每个测试用例的第一行包含两个整数 n 和 m（1 <= n, m <= 75），表示田地的大小，接下来的 n 行，每行包含 m 个 0-9 之间的数字，表示每块位置的价值。
输出描述:
输出一行表示牛牛所能取得的最大的价值。
示例1
输入
4 4
3332
3233
3332
2323
输出
2
```

#### 分析

- 使用二分查找来搜索能满足条件的最大值。
- 对每一个值k，判断其是否存在一种划分，能让他是最小的那一块。
  - 对于列的划分，使用三个变量进行循环
  - 对于行，则是在列的基础上计算出能满足和大于k的最小的划分，如果能划分出四行及以上，则证明这个k是可以得到的，接下来调整二分查找范围`left=mid+1`，否则`right=mid-1`

- 和的计算：可以计算从`[0,0]`到对应位置的范围和，然后有：`f(x1,y1,x2,y2) =f(x2,y2)-f(x1-1,y2)-f(x2,y1-1)+f(x1-1,y1-1) `
- 在循环体中需要尽可能地进行和的值的判断来剪枝，不然会超出时间要求

```python

def calc_sum(x1,y1,x2,y2,val_sum):
    return val_sum[x2][y2] - val_sum[x1-1][y2] - val_sum[x2][y1-1] + val_sum[x1-1][y1-1]

def check_valid(val_sum,k,M,N):
    for y1 in range(1,N-2):
        if calc_sum(1, 1, M, y1, val_sum) < k*4:continue
        for y2 in range(y1+1,N-1):
            if calc_sum(1, y1+1, M, y2, val_sum) < k*4:continue
            for y3 in range(y2+1,N):
                if calc_sum(1, y2+1, M, y3, val_sum) < k*4:continue
                if calc_sum(1, y3+1, M, N, val_sum) < k*4:continue
                split_part = 0
                last_part = 1
                for x in range(1,M+1):
                    # 选用x轴后，这四块都满足和大于k
                    if calc_sum(last_part,1,x,y1, val_sum) >= k and calc_sum(last_part,y1+1,x,y2, val_sum) >= k and calc_sum(last_part,y2+1,x,y3, val_sum) >= k and calc_sum(last_part,y3+1,x,N, val_sum) >= k:
                        split_part += 1
                        #设定该x轴，然后继续向右遍历，看还有几个x轴的划分能满足条件
                        last_part = x+1
                    #能划分出4列满足条件的，则返回true
                    if split_part >= 4:
                        return True
    return False

[M,N] = map(int,input().split())
nums=[list(map(int,list(input().strip()))) for _ in range(M)]

val_sum = [[0] * (N+1) for _ in range(M+1)]
for i in range(1,M+1):
    for j in range(1,N+1):
        val_sum[i][j] = val_sum[i][j-1] + val_sum[i-1][j] - val_sum[i-1][j-1] + nums[i-1][j-1]

res = 0
left,right = 0,val_sum[-1][-1]
while left <= right:
    mid = (left + right )//2
    if(check_valid(val_sum,mid,M,N)):
        left = mid + 1
        res = max(res,mid)
    else:
        right = mid - 1
        
print(res)
```

```c++
#include<bits/stdc++.h>
using namespace std;

int nums[100][100],sums[100][100];


int calc_sum(int x1,int y1,int x2,int y2)
{
    return sums[x2][y2]-sums[x1-1][y2]-sums[x2][y1-1]+sums[x1-1][y1-1];
}


bool check_valid(int k,int M,int N)
{
    for(int y1 = 1;y1<=N-3;y1++)
    {
        for(int y2 = y1+1;y2<=N-2;y2++)
        {
            for(int y3=y2+1;y3<=N-1;y3++)
            {
                int split_part=0,last_part=1;
                for(int x=1;x<=M;x++)
                {
                    if(calc_sum(last_part, 1,x,y1)>=k && calc_sum(last_part,y1+1,x,y2)>=k && calc_sum(last_part, y2+1,x,y3)>=k && calc_sum(last_part, y3+1,x,N)>=k)
                    {
                        last_part = x+1;
                        split_part += 1;
                    }
                    if(split_part>=4)
                        return true;
                }
            }
        }
    }
    return false;
}


int main()
{
    int N,M,res=0;
    cin >> M >> N;
    memset(sums,0,sizeof(sums));
    string s;
    for (int i = 0;i< M;i++)
    {
        cin >> s;
        for (int j = 0; j<s.length();j++)
            nums[i][j] = s[j]-'0';
    }

    for(int i=1;i<=M;i++)
        for (int j=1;j<=N;j++)
            sums[i][j] = sums[i-1][j] + sums[i][j-1]-sums[i-1][j-1]+nums[i-1][j-1];

    int left=0,right=sums[M][N];
    while(left <= right)
    {
        int mid = (left+right)/2;
        if(check_valid(mid,M,N))
        {
            left = mid + 1;
            res = max(res,mid);
        }
        else
            right = mid - 1;
    }
    cout << res<<endl;
}
```

