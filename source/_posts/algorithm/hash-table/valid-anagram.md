---
title: 有效的字母异位词
date: 2022-03-05
tags: ["哈希表"]
categories: ["算法"]
author: a东
---

## 有效的字母异位词
给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

注意：若 s 和 t 中每个字符出现的次数都相同，则称 s 和 t 互为字母异位词。
[ leetcode 题目链接](https://leetcode-cn.com/problems/valid-anagram/)

示例1
```
输入: s = "anagram", t = "nagaram"
输出: true  
```

示例2
```
输入: s = "rat", t = "car"
输出: false
```
<!-- more -->

### 解题思路
借助 `hashmap` 记录字符串中每个字符出现的次数，进行比对得到结果。注意第二轮比对时一但某个字符的记录数减为 `0` 就从 `hashmap` 中删除，最后根据 `hashmap` 的长度判断结果。


```cgo
    func isAnagram(s string, t string) bool {
        if len(s) != len(t) {
            return false
        }
    
        chMap := make(map[rune]int)
        for _, ch := range s {
            chMap[ch]++
        }
    
        for _, ch := range t {
            if chMap[ch] > 0 {
                chMap[ch]--
                if chMap[ch] == 0 {
                    delete(chMap, ch)
                }
            } else {
                return false
            }
        }
    
        return len(chMap) == 0
    }
```


### 复杂度分析
- 时间复杂度：O(m+n)，其中 m+n 是2个字符串的长度。
- 空间复杂度：O(m+n)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/valid-anagram/solution/you-xiao-de-zi-mu-yi-wei-ci-by-leetcode-solution/)






