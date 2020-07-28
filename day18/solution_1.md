### [shopee的零食柜](<https://www.nowcoder.com/practice/24a1bb82b3784f86babec24e4a5c93e0?tpId=179&&tqId=34271&rp=1&ru=/ta/exam-other&qru=/ta/exam-other/question-ranking>)

   shopee的零食柜，有着各式各样的零食，但是因为贪吃，小虾同学体重日益增加，终于被人叫为小胖了，他终于下定决心减肥了，他决定每天晚上去操场跑两圈，但是跑步太累人了，他想转移注意力，忘记痛苦，正在听着音乐的他，突然有个想法，他想跟着音乐的节奏来跑步，音乐有7种音符，对应的是1到7，那么他对应的步长就可以是1-7分米，这样的话他就可以转移注意力了，但是他想保持自己跑步的速度，在规定时间m分钟跑完。为了避免被累死，他需要规划他每分钟需要跑过的音符，这些音符的步长总和要尽量小。下面是小虾同学听的歌曲的音符，以及规定的时间，你能告诉他每分钟他应该跑多少步长？

```
输入描述:
输入的第一行输入 n（1 ≤ n ≤ 1000000，表示音符数），m（1<=m< 1000000, m <= n）组成，
第二行有 n 个数，表示每个音符（1<= f <= 7）
输出描述:
输出每分钟应该跑的步长
示例1
输入
8 5 6 5 6 7 6 6 3 1
输出
11
```

#### 分析

- 思路是把所有的音符划分成`m`份，然后保证这`m`份中的和的最小值越小越好
- 二分法，遍历不同的步长step

```python
def calc_valid(nums,max_minute,cur_step):
    need_minute = 0
    cur_length = 0
    for val in nums:
        if cur_length + val > cur_step:
            need_minute += 1
            cur_length = val
        else:
            cur_length += val
    if cur_length != 0:need_minute +=1
    if need_minute <= max_minute:
        return True
    return False

N, M = list(map(int,input().split()))
vals = list(map(int,input().split()))

mid = 0
left,right =7,sum(vals)
while left <= right:
    mid = (left+right)//2
    if calc_valid(vals.copy(), M, mid):
        right = mid - 1
    else:
        left = mid + 1
print(mid)
```

