## day 09

### 1. [贪心的小博](<https://www.nowcoder.com/practice/0b9057782d064aeca1897bc1cfda4092?tpId=128&&tqId=33805&rp=1&ru=/ta/exam-meituan&qru=/ta/exam-meituan/question-ranking>)
小博沉迷收集卡片，购买干脆面是他收集卡片的主要方式。他总共渴望的有N类卡片，均可通过购买干脆面获得，一包干脆面中有且仅有一张卡片，并且卡片类型对应N类卡片中的一种。且每 种类型的卡片出现在一包干脆面中的概率是相等的。 
小博非常的贪心，他有N个愿望，第i个愿望即为:拥有至少pi张i类卡片，其中1 ≤ i ≤ N。              

然而，小博又极其贫困，他想知道最少需要买多少干脆面，使得在最坏情况下，至少能够满足他 N个愿望的其中一个。

```
输入描述:
第一行包含一个整数N， 1 ≤ N ≤ 105。
第二行包含N个整数pi，pi表示小博希望至少拥有的i类卡片数量。1 ≤ pi ≤ 105。
输出描述:
输出一个整数ANS，小博可以完成至少一个愿望需要购买的最少的干脆面的数量。
示例1
输入
3
8 6 9
输出
21
示例2
输入
2
3 5
输出
7
```

#### [题解链接](./solution_1.md)

### 2. [种花](<https://www.nowcoder.com/practice/09066b2c010f4218adb1a1db42dbb236?tpId=128&&tqId=33814&rp=1&ru=/ta/exam-meituan&qru=/ta/exam-meituan/question-ranking>)

题目给定a1,a2...an，这样一个长度为n的序列，现在你可以给其中一些元素加上一个值x（只能加一次），然后可以给另外一公园里有N个花园，初始时每个花园里都没有种花，园丁将花园从1到N编号并计划在编号为i的花园里恰好种A_i朵花，他每天会选择一个区间[L，R]（1≤L≤R≤N）并在编号为L到R的花园里各种一朵花，那么园丁至少要花多少天才能完成计划？

```
输入描述:
第一行包含一个整数N，1≤N≤10^5。

第二行包含N个空格隔开的整数A_1到A_N，0≤A_i≤10^4。
输出描述:
输出完成计划所需的最少天数。
示例1
输入
5
4 1 8 2 5
输出
14
```

#### [题解链接](./solution_2.md)

### 3.[友好城市](<https://www.nowcoder.com/practice/d5a28292e62c4419a145ed6ba2656450?tpId=128&&tqId=33790&rp=1&ru=/ta/exam-meituan&qru=/ta/exam-meituan/question-ranking>)

![](https://uploadfiles.nowcoder.com/images/20180605/303792_1528168267595_9BB1871DD92F37E2F38C4873EAF7C267)

![](https://uploadfiles.nowcoder.com/images/20180605/303792_1528168245042_79474D3F3C2CD1791B68D7CC03624AE1)

```
输出：最小匹配代价
输入
4
-1 2 -1 10
2 -1 3 -1
-1 3 -1 1
10 -1 1 -1
2
1 2 3 4
输出
3
```

#### [题解链接](./solution_3.md)

