### [末尾0的个数](<https://www.nowcoder.com/practice/6ffdd7e4197c403e88c6a8aa3e7a332a?tpId=152&&tqId=33988&rp=1&ru=/ta/exam-didi&qru=/ta/exam-didi/question-ranking>)

输入一个正整数n,求n!(即阶乘)末尾有多少个0？ 比如: n = 10; n! = 3628800,所以答案为2

```
输入描述:
输入为一行，n(1 ≤ n ≤ 1000)
输出描述:
输出一个整数,即题目所求
示例1
输入
10
输出
2
```

#### 分析

对于25、125等值可以分解质因数，在阶乘时构造出多个5。

`对任意正实数x，n是正整数，则从1到x的整数中，n的倍数有[x/n]个`

一直通过除法取整，可以计算出包含多个质因子5的数的个数。

```
[0,100]: 为5的倍数的数字个数：100/5 = 20
[0,100]: 为25的倍数的数字个数：20/5 = 4   [25,50,75,100]
```

```python
N = int(input())

res = 0
while N != 0:
    N = N//5
    res += N
print(res)
```

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args)
    {
        Scanner in = new Scanner(System.in);
        
        int a = in.nextInt();
        int res = 0;
        while (a != 0)
        {
            a /= 5;
            res += a;
        }
        System.out.println(res);
    }
}
```

