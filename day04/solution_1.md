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

#### 