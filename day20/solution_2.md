### [分石头](<https://www.nowcoder.com/practice/343e8ccf80474ef686005d95637dd08d?tpId=179&&tqId=34185&rp=1&ru=/ta/exam-other&qru=/ta/exam-other/question-ranking>)

已知石头重量数组。将石头分为质量最接近的两组

```
输入描述:
数组，值为每个石头的质量
输出描述:
两组的质量（降序排序）
示例1
输入
5,1,1,1,1,1
输出
5,5
备注:
质量限定为 Integer
```

- 求和之后取其中值，然后作为0-1背包问题来计算。

```C++
#include<bits/stdc++.h>
using namespace std;

int main()
{
    string s;
    cin >> s;
    vector<int> nums;
    for(int i = 0;i<s.length();i+=2)
        nums.push_back((int)(s[i]-'0'));
    sort(nums.begin(), nums.end());

    int sum = 0;
    for(auto v:nums)
        sum += v;
    
    if (nums.size() == 1)
    {
        cout << nums[0]<<","<<0<<endl;
        return 0;
    }
    else if(nums.size()==2)
    {
        cout<<nums[1]<<","<<nums[0]<<endl;
        return 0;
    }
    //最大值为target的0-1背包问题
    int target = sum / 2;
    vector<int> dp(target+1,0);
    for(int i=0;i!=nums.size();i++)
        for (int j = target;j>=nums[i];j--)
            if (dp[j] < dp[j-nums[i]]+nums[i])
                dp[j] = dp[j-nums[i]]+nums[i];
    cout << sum - dp[target] << "," << dp[target];
}

```

