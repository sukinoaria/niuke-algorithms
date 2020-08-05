### [相邻最大差值](<https://www.nowcoder.com/practice/376ede61d9654bc09dd7d9fa9a4b0bcd?tpId=179&&tqId=34130&rp=1&ru=/ta/exam-other&qru=/ta/exam-other/question-ranking>)

请设计一个复杂度为O(n)的算法，计算一个未排序数组中排序后相邻元素的最大差值。

```
给定一个整数数组A和数组的大小n，请返回最大差值。保证数组元素个数大于等于2小于等于500。
测试样例：
[9,3,1,10],4
返回：6
```

#### 分析

使用桶来计数每个值是不是存在，然后再遍历一次这个桶，中途记录下离得最远的桶的距离，这个距离加1就是最大的元素差。

```c++
#include<bits/stdc++.h>
using namespace std;

class MaxDivision {
public:
    int findMaxDivision(vector<int> A, int n) {
        int max = *max_element(A.begin(),A.end());
        vector<int> buckets(max+1,0);
        for(auto i = A.begin();i!=A.end();i++)
            buckets[*i] = 1;
        auto j = buckets.begin();
        while(*j == 0) j++;
        int cnt = 0;
        int max_cnt = 0;
        for(;j!=buckets.end();j++)
        {
            if(*j != 0)
            {
                cnt = 0;
                continue;
            }
            else {
                cnt += 1;
                max_cnt = cnt > max_cnt ? cnt : max_cnt;
            }
        }
        return max_cnt+1;
    }
};
```

