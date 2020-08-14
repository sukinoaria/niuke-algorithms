## day 04

### JZ10. 矩形覆盖
我们可以用`2*1`的小矩形横着或者竖着去覆盖更大的矩形。请问用n个`2*1`的小矩形无重叠地覆盖一个`2*n`的大矩形，总共有多少种方法？

比如`n=3`时，`2*3`的矩形块有3种覆盖方法：

![](https://uploadfiles.nowcoder.com/images/20200218/6384065_1581999858239_64E40A35BE277D7E7C87D4DCF588BE84)

#### 分析

其实质还是Fibonacci数列，因为小矩形为`2*1`，对一个更大的矩形`2*n`，也只需要考虑`n-1`和`n-2`的情况，其他的情况已经包含在里面了。

```python
# -*- coding:utf-8 -*-
class Solution:
    def rectCover(self, number):
        # write code here
        if number < 3:return number
        a,b = 1,2
        while number > 2:
            a,b = b,a+b
            number -= 1
        return b
```

### JZ11. 二进制中1的个数
输入一个整数，输出该数32位二进制表示中1的个数。其中负数用补码表示。

#### 分析

考点是位运算操作

- 在Python中整型是无限长的，为了方便计算负数，先通过`n & 0xffffffff`求得了一个新的数值(该数值前面有无限个0.之后的值和原先n的补码一样，但是两个数并不相同)
- 之后再通过与运算计算：
  - 思路一：n逐次与1进行`&`操作(最右边为1的话结果为1),然后n左移直到n=0.
  - `n & (n-1)`该操作可以将原整数最右边的1变为零，有多少个1就进行几次操作，操作次数更少。

```python
# -*- coding:utf-8 -*-
class Solution:
    def NumberOf1(self, n):
        # write code here
        if n < 0:
            n = n & 0xffffffff
        cnt = 0
        while n:
            cnt += n & 1
            n >>= 1
        return cnt
```

```python
# -*- coding:utf-8 -*-
class Solution:
    def NumberOf1(self, n):
        # write code here
        if n < 0:
            n = n & 0xffffffff
        cnt = 0
        while n:
            n = n&(n-1)
            cnt += 1
        return cnt
```

### JZ12.数值的整数次方

给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

保证base和exponent不同时为0

#### 分析

快速幂算法：

- 基础情况：`exp=0`时结果为1，`base=0`时结果为0
- 当`exp`为偶数，则`base^exp = base^(exp/2) * base^(exp/2)`
- 当`exp`为奇数，则`base^exp = base^(exp-1/2) * base^(exp-1/2)*base`

```python
# -*- coding:utf-8 -*-
class Solution:
    def Power(self, base, exponent):
        # write code here
        if base == 0 :
            return 0
        elif exponent == 0:
            return 1
        exp = exponent if exponent > 0 else -exponent
        res = 1
        base_exp = base
        while exp > 0:
            if exp & 1 == 1:
                res *= base_exp
            exp >>= 1
            base_exp *= base_exp
        return res if exponent > 0 else 1/res
```

- 递归方式

```python
# -*- coding:utf-8 -*-
class Solution:
    def Power(self, base, exponent):
        # write code here
        if base == 0 :
            return 0
        exp = exponent if exponent > 0 else -exponent
        memo = [-1] * (exp+1)
        def helper(base,exp):
            if memo[exp]!=-1:
                return memo[exp]
            elif exp == 0:
                memo[exp] = 1
            elif exp == 1:
                memo[exp] = base
            else:
                memo[exp] = helper(base, exp>>1)
                memo[exp] *= memo[exp]
                if exp & 1:
                    memo[exp] *= base
            return memo[exp]
        res = helper(base,exp)
        return res if exponent > 0 else 1/res
        
```

