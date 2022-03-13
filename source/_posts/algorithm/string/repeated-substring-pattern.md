---
title:  重复的子字符串
date: 2022-03-13
tags: ["字符串"]
categories: ["算法"]
author: a东
---

##  重复的子字符串
给定一个非空的字符串 s ，检查是否可以通过由它的一个子串重复多次构成。

[leetcode 题目链接](https://leetcode-cn.com/problems/repeated-substring-pattern/)

示例1
```
输入: s = "abab"
输出: true
解释: 可由子串 "ab" 重复两次构成。
```

示例2
```
输入: s = "aba"
输出: false
```

<!-- more -->

示例3
```
输入: s = "abcabcabcabc"
输出: true
解释: 可由子串 "abc" 重复四次构成。 (或子串 "abcabc" 重复两次构成。)
```

### 解题思路1
枚举每个可能的子串长度进行验证，子串的长度最长不超过原字符串长度的一半。

```cgo
    func repeatedSubstringPattern(s string) bool {
        for subLen := 1; subLen <= len(s)/2; subLen++ { // 枚举每个可能长度的子字符串进行匹配验证
            if len(s) % subLen != 0 { // 必然不满足
                continue
            }
            
            exist := true
            for i := 0; i < len(s) / subLen; i++ { // 每轮验证一个子字符串
                for j := 0; j < subLen; j++ { // 一轮
                    if s[j] != s[i*(subLen-1)+i+j] { // 注意下标对应关系
                        exist = false
                        break
                    }
                }
                if !exist {
                    break
                }
            }
    
            if exist {
                return true
            }
        }
        return false
    }
```


### 复杂度分析
- 时间复杂度：O(n^2)，其中 n 是字符串长度。
- 空间复杂度：O(1)。


### 解题思路2
KMP算法...


## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/repeated-substring-pattern/solution/zhong-fu-de-zi-zi-fu-chuan-by-leetcode-solution/)






