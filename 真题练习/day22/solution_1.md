### [简单表达式运算](<https://www.nowcoder.com/practice/6221faa383fc49f1b10dffcb62c866bf?tpId=149&&tqId=33973&rp=1&ru=/ta/exam-bilibili&qru=/ta/exam-bilibili/question-ranking>)

给定一个合法的表达式字符串，其中只包含非负整数、加法、减法以及乘法符号（不会有括号），例如7+3*4*5+2+4-3-1，请写程序计算该表达式的结果并输出；

```
输入描述:
输入有多行，每行是一个表达式，输入以END作为结束
输出描述:
每行表达式的计算结果
示例1
输入
7+3*4*5+2+4-3-1
2-3*1
END
输出
69
-1
备注:
每个表达式的长度不超过10000，保证所有中间结果和最后结果在[-2e9,2e9]范围内
```

#### 思路

- 先计算高优先级的运算符，之后在计算低优先级的，分两次使用栈和队列计算。
- 首先是对数字字符串的处理，将含多个位的数字字符串进行合并。

```python
from collections import deque
while True:
    try:
        e_str = input()
        if e_str.strip() == "END":break
        equation = []
        for i in range(len(e_str)):
            if e_str[i].isdigit():
                if len(equation)==0 or not equation[-1].isdigit():
                    equation.append(e_str[i])
                else: equation[-1]+=e_str[i]
            else:
                equation.append(e_str[i])
        
        i  = 0
        que = deque()
        while i < len(equation):
            if equation[i] == '*' or equation[i]=='/':
                pre = que.pop()
                if equation[i] == '*':
                    que.append(int(pre) * int(equation[i+1]))
                else:
                    que.append(int(pre) // int(equation[i+1]))
                i += 2
            else:
                que.append(equation[i])
                i+= 1
        stack = []
        while que:
            cur = que.popleft()
            if cur != '+' and cur != '-':
                stack.append(cur)
            else:
                pre = stack.pop()
                nex = que.popleft()
                if cur == '+':
                    stack.append(int(pre) + int(nex))
                else:
                    stack.append(int(pre) - int(nex))
        print(int(stack[0]))
    except:
        break
```

