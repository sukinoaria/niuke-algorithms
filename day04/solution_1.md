### [百分号解码](<https://www.nowcoder.com/questionTerminal/79c892f6001b49d5a0680716e6f4f14d>)
来源：[深信服校园招聘算法练习卷](<https://www.nowcoder.com/test/23358504/summary>)

在URL字符串中，如果百分号%后面跟了两个十六进制数字，那么它表示相应ASCII值所对应的字符，如%2F表示'/'，%32表示'2'。%编码还可以进行嵌套，如%%32F可以解码成%2F，再进一步解码成/。如果没有任何百分号后面跟的是两个十六进制数字则无法再进行解码。

现在有一系列的URL，小强希望你帮忙进行百分号解码，直到无法再解码为止。

```
输入描述:
第一行一个正整数T（T<=10），表示T个测试样例；
对于每个测试样例，
输入字符串s，字符串不包含空白符且长度小于100,000。

有部分测试样例的字符串长度<=1,000。

输出描述:
输出T行，每行一个字符串，表示解码后的结果。
示例1
输入
1
%%32F
输出
/
```

####  分析

- 思路：倒着对字符串进行遍历，并使用栈来存储遍历的字符，当遇到`%`时弹出两个值来组合成新的字符，如果组合成的新字符是`%`的话重复进行解码，否则送入栈中，继续遍历。

```python

def decode(stack):
    val1 = stack.pop()
    val2 = stack.pop()
    ch = chr(int(val1+val2,16))
    if ch == '%':
        stack = decode(stack)
    else:
        stack.append(ch)
    return stack
    
def main():
    N = int(input())
    for i in range(N):
        s = str(input())
        stack = []
        for c in s[::-1]:
            if c != '%':
                stack.append(c)
            else:
                stack = decode(stack)
        print("".join(stack[::-1]))
main()
```

