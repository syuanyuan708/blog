---
title:  反转字符串
date: 2022-03-12
tags: ["字符串"]
categories: ["算法"]
author: a东
---

##  反转字符串
编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 s 的形式给出。

不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。
[leetcode 题目链接](https://leetcode-cn.com/problems/reverse-string/)

示例1
```
输入：s = ["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```

示例2
```
输入：s = ["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```
<!-- more -->

### 解题思路
用2个指针从字符串的首尾向中间逼近，并在迭代过程中交换字符。


```cgo
    func reverseString(s []byte)  {
        left := 0
        right := len(s) - 1
    
        for left < right {
            s[left], s[right] = s[right], s[left]
            left++
            right--
        }
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是字符串长度。
- 空间复杂度：O(1)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/reverse-string/solution/fan-zhuan-zi-fu-chuan-by-leetcode-solution/)






