###  [重复串查找](<https://www.nowcoder.com/questionTerminal/33d378140e084df9adbbb88eacf34e50?answerType=1&f=discussion>)
来源：[深信服校园招聘算法练习卷](<https://www.nowcoder.com/test/23358504/summary>)

一个重复字符串是由两个相同的字符串首尾拼接而成，例如abcabc便是长度为6的一个重复字符串，而abcba则不存在重复字符串。
给定任意字符串，请帮小强找出其中的最长重复子串。

```
输入描述:
输入一个字符串s，其中s长度小于1e4而且只包含数字和字母。

输出描述:
输出一个整数，表示s的最长重复子串长度，若不存在则输出0
示例1
输入
xabcabcx
输出
6
```

- 分析：使用不同长度去原句中遍历是否可行，对长度的搜索使用二分查找。AC80，之后有空再看看。

```python
def check_valid(s,length):
     
    for i in range(len(s)):
        if i+length < len(s) and s[i] == s[i+length]:
            if i + length * 2 <= len(s):
                if s[i:i+length] == s[i+length:i+2*length]:
                    return True
    return False
         
def main():
    s = input()
    left,right = 0,len(s)//2+1
    max_length = 0
    while left <= right:
        mid = (left+right)//2
        if check_valid(s, mid): 
            max_length = max(max_length,mid)
            left = mid  + 1
        else:
            right = mid - 1
    
    return max_length*2 if 0 < max_length < len(s) else 0
print(main())
```

