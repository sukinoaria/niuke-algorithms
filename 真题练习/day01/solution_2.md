### [击败魔物](<https://www.nowcoder.com/questionTerminal/e93f31a0387b40e88a53e55b8ab703f8?answerType=1&f=discussion>)

来源：[小红书2020校招算法笔试题卷一](<https://www.nowcoder.com/test/23568027/summary>)

> 时间限制：C/C++ 1秒，其他语言2秒
>
> 空间限制：C/C++ 256M，其他语言512M

薯队长来到了迷宫的尽头，面前出现了N只魔物，Hi表示第i只魔物的血量，薯队长需要在T个回合内击败所有魔物才能获胜。每个回合薯队长可 以选择物理攻击一只魔物，对其造成1点伤害（物理攻击次数无上限）;

或者消耗1点法力释放必杀技对其造成固定X点伤害（薯队长开始拥有M 点法力）。问X至少多大，薯队长才有机会获胜；如果无论如何都无法在T回合内获胜，则输出-1 

```
输入描述:
第一行三个整数分别表示：N，T，M 第二行有N个整数：H1，H2，H3...HN 

输出描述:
输出一个整数，表示必杀技一次最少造成多少固定伤害 

输入例子1:
3 4 3
5 2 1

输出例子1:
3
```

---

### 分析

考察点：二分搜索、贪心

- 思路：沿着`[0,max_hp]`的范围搜索最合适的伤害值，注意对一些特殊情形的处理。
- 使用函数`check_valid`判断当前技能伤害能否过关
  - 首先是根据法力值的大小先对整体的怪物进行伤害，**只求打满最大的伤害而不去补刀**
  - 之后根据剩余的血量重排序，此时：
    - 如果没有了法力值，则只需要判断血量和是不是大约剩余轮数。
    - 如果剩余法力值，则根据重排序的结果，**优先清掉血量高的怪物**，之后再判断剩余的轮数够不够清掉所有的怪物。

```python
def check_valid(num, turn, magic, hps, damage):
    # 使用技能造成伤害但不补刀，最后剩下法力值的时候在进行补刀
    i = 0
    for i in range(num):
        # 释放技能的次数为整除的次数或者是魔力值的次数，取小的那个
        
        spell_time = min(hps[i] // damage, magic)
        hps[i] -= spell_time * damage
        turn -= spell_time
        magic -= spell_time
        if magic == 0: break
    # 去除刚好整除的值
    
    hps = sorted(hps)
    i = 0
    if hps[-1] == 0:return True
    while hps[i] == 0:
        i += 1
    hps = hps[i:]
    # 普攻或者技能能够清掉
    
    if sum(hps) <= turn : return True
    if len(hps) <= magic:
        return True
    
    # 还剩余法力值，此时怪物的血量必定都小于技能伤害，按血量从高到低使用技能
    
    else:
        last = len(hps) - 1
        while magic > 0:
            last -= 1
            magic -= 1
            turn -= 1
        # 无法力值，判断能否用普攻清完
        
        hps = hps[:last+1]
        return turn >= sum(hps)


def main():
    num, turn, magic = list(map(int, input().split()))
    hps = list(map(int, input().split()))

    #回合不够必定输
    
    if len(hps) > turn: return -1
    
    # 法力值为零且血量和大于回合数 必定输
    if magic == 0 and sum(hps) > turn: return -1
    
    left, right = 0, int(max(hps))
    while left < right:
        mid = (left + right) // 2
        # 注意python浅拷贝的坑
        
        if check_valid(num, turn, magic, hps.copy(), damage=mid):
            right = mid
        else:
            left = mid+1
    # 如果left = max(hps)，同样是不存在伤害值满足条件，left一直右移直到越界
    
    return left if left < max(hps) else -1

print(main())
```

