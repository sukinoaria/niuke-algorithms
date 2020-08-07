### [爬楼梯2](<https://www.nowcoder.com/practice/1e6ac1a96c3149348aa9009709a36a6f?tpId=125&&tqId=33764&rp=1&ru=/ta/exam-xiaomi&qru=/ta/exam-xiaomi/question-ranking>)

在你面前有一个n阶的楼梯(n>=100且n<500)，你一步只能上1阶或3阶。
请问计算出你可以采用多少种不同的方式爬完这个楼梯（到最后一层为爬完）。
(注意超大数据)

```
输入描述:
一个正整数，表示这个楼梯一共有多少阶
输出描述:
一个正整数，表示有多少种不同的方式爬完这个楼梯
示例1
输入
100
输出
24382819596721629
备注:
注意时间限制
```

#### 分析

简单题，

- `f(i) = f(i-1) + f(i-3)`

- 初始条件：第一处和第二处台阶只有1种，第三处有两种。

```python
N = int(input())

dp = [0] * N

dp[0] = 1
dp[1] = 1
dp[2] = 2
for i in range(3,N):
    dp[i] = dp[i-3]+dp[i-1]
print(dp[-1])
```

- Java需要使用`BigInteger`类。  **果然Python是世界上最好的语言 **
- 且Java没有重载常见的运算符，需要使用成员函数`.add`等进行运算。

```java
import java.util.Scanner;
import java.math.BigInteger;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        int N = in.nextInt();
        BigInteger[] dp = new BigInteger[N];
        dp[0] = new BigInteger("1");
        dp[1] = new BigInteger("1");
        dp[2] = new BigInteger("2");
        for (int i = 3;i<N;i++)
        {
            dp[i] = dp[i-1].add(dp[i-3]);
        }
        System.out.println(dp[N-1]);
    }
}
```

