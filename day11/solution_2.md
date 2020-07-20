### [连续最大和](<https://www.nowcoder.com/practice/5a304c109a544aef9b583dce23f5f5db?tpId=152&&tqId=33985&rp=1&ru=/ta/exam-didi&qru=/ta/exam-didi/question-ranking>)

一个数组有 N 个元素，求连续子数组的最大和。 例如：[-1,2,1]，和最大的连续子数组为[2,1]，其和为 3

```
输入描述:
输入为两行。 第一行一个整数n(1 <= n <= 100000)，表示一共有n个元素 第二行为n个数，即每个元素,每个整数都在32位int范围内。以空格分隔。
输出描述:
所有连续子数组中和最大的值。
示例1
输入
3 -1 2 1
输出
3
```

#### 分析

动态规划，在第`i`处的转移条件：`i-1`处的最大和加上`nums[i]`大于`nums[i]`时，考虑将`i`处的数作为子数组的一部分，否则重新开始计算子数组。

`f(i) = max( f(i-1)+nums[i] , nums[i] )`

```python
N = int(input())
nums = list(map(int,input().split()))

dp = [0] * N
dp[0] = nums[0]

#之后直接从第2个元素开始比较
max_val = nums[0]

for i in range(1,N):
    dp[i] = max(dp[i-1]+nums[i],nums[i])
    max_val = max(dp[i],max_val)
print(max_val)
```

```java
import java.util.Scanner;

public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        int N = in.nextInt();
        int[] nums = new int[N];
        for (int i = 0;i < N;i++)
        {
            nums[i] = in.nextInt();
        }
        int max = nums[0];
        int sum = nums[0];
        for(int i =1;i<N;i++){
            if (sum > 0)
                sum += nums[i];
            else
                sum = nums[i];
            if (sum > max)
                max = sum;
        }
        System.out.println(max);
    }
}
```

