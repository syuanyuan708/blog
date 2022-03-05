---
title: 快乐数
date: 2022-03-05
tags: ["哈希表"]
categories: ["算法"]
author: a东
---

## 快乐数
编写一个算法来判断一个数 n 是不是快乐数。

「快乐数」 定义为：

对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。
如果这个过程 结果为 1，那么这个数就是快乐数。
如果 n 是 快乐数 就返回 true ；不是，则返回 false 。
[ leetcode 题目链接](https://leetcode-cn.com/problems/happy-number/)

示例1
```
输入：n = 19
输出：true
解释：
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```
<!-- more -->
示例2
```
输入：n = 2
输出：false
```


### 解题思路
按照快乐数的规则对给定的数 `n` 进行运算，如何运算过程中出现结果为 `1` 那么这个数就是快乐数，如果运算过程中出现了值为 `n` 的结果那运算过程就会不断重复，这个数就不是快乐数。对于过程中是否出现结果等于 `n` 的运算可以使用 `hashmap` 来记录每次运算得到的结果。


```cgo
    func isHappy(n int) bool {
        happyMap := make(map[int]bool)
    
        for {
            res := powSum(n)
            if res == 1 {
                return true
            }
            if happyMap[res] {
                return false
            } else {
                happyMap[res] = true
            }
    
            n = res
        }
        return false
    }
    // 计算下一个数
    func powSum(n int) int {
        res := 0
        for n != 0 {
            res += (n % 10)*(n % 10)
            n = n / 10
        }
        return res
    }
```


### 复杂度分析
- 时间复杂度：O(log n)，其中 n 是给定整数的位数，每一轮的计算代价为 log n 具体计算可以参考 leetcode。
- 空间复杂度：O(log n)，与时间复杂度对应，每一轮需要空间 O(1)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/happy-number/solution/kuai-le-shu-by-leetcode-solution/)






