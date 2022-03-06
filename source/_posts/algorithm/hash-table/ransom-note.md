---
title:  赎金信
date: 2022-03-05
tags: ["哈希表"]
categories: ["算法"]
author: a东
---

##  赎金信
给你两个字符串：ransomNote 和 magazine ，判断 ransomNote 能不能由 magazine 里面的字符构成。

如果可以，返回 true ；否则返回 false 。

magazine 中的每个字符只能在 ransomNote 中使用一次。
[ leetcode 题目链接](https://leetcode-cn.com/problems/ransom-note/)

示例1
```
输入：ransomNote = "a", magazine = "b"
输出：false
```

示例2
```
输入：ransomNote = "aa", magazine = "ab"
输出：false
```
<!-- more -->

示例3
```
输入：ransomNote = "aa", magazine = "aab"
输出：true
```

### 解题思路
用2个 `hashtable` 统计每个字符串中字符出现的次数，然后比较2个 `hashtable` 来判断能不能满足题目要求即可。

```cgo
    func canConstruct(ransomNote string, magazine string) bool {
        rMap := make(map[rune]int)
        for _, ch := range ransomNote {
            rMap[ch]++
        }
    
        sMap := make(map[rune]int)
        for _, ch := range magazine {
            sMap[ch]++
        }
    
        for ch, cnt := range rMap {
            if cnt > sMap[ch] {
                return false
            }
        }
    
        return true
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是字符串的长度。
- 空间复杂度：O(n)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/ransom-note/solution/shu-jin-xin-by-leetcode-solution-ji8a/)






