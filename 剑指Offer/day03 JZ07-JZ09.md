## day 03

### JZ7. 斐波那契数列
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0，第1项是1），其中n<=39。

#### 分析

可用动态规划、递归等方法，也可以选择将递归转为迭代，并只使用两个变量，空间复杂度`O(1)`

```python
# -*- coding:utf-8 -*-
class Solution:
    def Fibonacci(self, n):
        if n == 0:return 0
        a,b = 0,1
        while n > 1:
            a,b = b,a+b
            n -= 1
        return b
```

### JZ8. 跳台阶
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

#### 分析

和上一题基本一致，只是对于n的定义不同，因此循环终止条件有所区别。

```python
# -*- coding:utf-8 -*-
class Solution:
    def jumpFloor(self, number):
        # write code here
        if number == 0:return 0
        a,b = 0,1
        while number > 0:
            a,b = b,a+b
            number -= 1
        return b
```

### JZ9. 变态跳台阶

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

#### 分析

相对于上题中的`f(i) = f(i-1)+f(i-2)`，此题中`f(i)=f(0)+f(1)+f(2)+...+f(i-1)`,用动态规划。`f(0)`代表的是一步跳`i`阶到达，所以初始化值为1.

```python
# -*- coding:utf-8 -*-
class Solution:
    def jumpFloorII(self, number):
        # write code here
        dp = [1]*(number+1)
        for i in range(2,number+1):
            dp[i] = sum(dp[:i])
        return dp[-1]
```

