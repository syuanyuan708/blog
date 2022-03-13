---
title:  实现 strStr()
date: 2022-03-13
tags: ["字符串"]
categories: ["算法"]
author: a东
---

##  实现 strStr()
实现 strStr() 函数。

给你两个字符串 haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串出现的第一个位置（下标从 0 开始）。如果不存在，则返回  -1 。

 

说明：

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与 C 语言的 strstr() 以及 Java 的 indexOf() 定义相符。
[leetcode 题目链接](https://leetcode-cn.com/problems/implement-strstr/)

示例1
```
输入：haystack = "hello", needle = "ll"
输出：2
```

示例2
```
输入：haystack = "aaaaa", needle = "bba"
输出：-1
```

<!-- more -->

示例3
```
输入：haystack = "", needle = ""
输出：0
```

### 解题思路1
暴力遍历匹配，直到找到第一个匹配的位置或遍历到字符串末尾。

```cgo
    func strStr(haystack string, needle string) int {
        if len(needle) == 0 {
            return 0
        }
    
        j := 0
        for i := 0; i < len(haystack); i++ {
            if haystack[i] == needle[j] {
                start := i
                res := start
                for start < len(haystack) && j < len(needle) && haystack[start] == needle[j] {
                    start++
                    j++
                }
                if j == len(needle) {
                    return res
                } else {
                    j = 0
                }
            }
            
        }
    
        return -1
    }
```


### 复杂度分析
- 时间复杂度：O(n*m)，其中 n, m 是2个字符串长度。
- 空间复杂度：O(1)。


### 解题思路2
KMP算法...


## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/implement-strstr/solution/shi-xian-strstr-by-leetcode-solution-ds6y/)






