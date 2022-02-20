---
title: 最小覆盖子串
date: 2022-02-20
tags: ["数组", "滑动窗口"]
categories: ["算法"]
author: a东
---

## 最小覆盖子串
给你一个字符串 s 、一个字符串 t 。返回 s 中涵盖 t 所有字符的最小子串。如果 s 中不存在涵盖 t 所有字符的子串，则返回空字符串 "" 。

[ leetcode 题目链接](https://leetcode-cn.com/problems/minimum-window-substring/)

示例1
```
输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC"
```

示例2
```
输入：s = "a", t = "a"
输出："a"
```
<!-- more -->

示例3
```
输入: s = "a", t = "aa"
输出: ""
解释: t 中两个字符 'a' 均应包含在 s 的子串中，因此没有符合条件的子字符串，返回空字符串。
```

### 解题思路
采用滑动窗口进行处理，用2个 `map` 存储待比较字符串的字符和对应个数，开始扩展窗口，一但满足覆盖字符串的条件则左指针开始移动来收缩窗口以寻找能满足覆盖条件的更小窗口。


```cgo
    func minWindow(s string, t string) string {
        start, end := 0, 0
        left, right := 0, 0
        sMap, tMap := map[byte]int{}, map[byte]int{}
        minLen := math.MaxInt32
    
        for i := 0; i < len(t); i++ {
            tMap[t[i]]++
        }
    
        for ; right < len(s); right++ {
            sMap[s[right]]++
            for isContain(sMap, tMap) {
                if right - left + 1 < minLen {
                    start, end = left, right
                    minLen = right - left + 1
                }
                sMap[s[left]]--
                left++
            }
        }
        if minLen == math.MaxInt32 {
            return ""
        }
        return s[start:end+1]
    }
    
    func isContain(sMap map[byte]int, tMap map[byte]int) bool {
        for k, v := range tMap {
            if v > sMap[k] {
                return false
            }
        }
        return true
    }
```

### 复杂度分析
- 时间复杂度：最坏情况下左右指针对 ss 的每个元素各遍历一遍，哈希表中对 ss 中的每个元素各插入、删除一次，对 tt 中的元素各插入一次。每次检查是否可行会遍历整个 tt 的哈希表，哈希表的大小与字符集的大小有关，设字符集大小为 CC，则渐进时间复杂度为 O(C\cdot |s| + |t|)O(C⋅∣s∣+∣t∣)。
- 空间复杂度：这里用了两张哈希表作为辅助空间，每张哈希表最多不会存放超过字符集大小的键值对，我们设字符集大小为 CC ，则渐进空间复杂度为 O(C)O(C)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/minimum-window-substring/solution/zui-xiao-fu-gai-zi-chuan-by-leetcode-solution/)






