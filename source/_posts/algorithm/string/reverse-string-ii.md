---
title:  反转字符串 II
date: 2022-03-12
tags: ["字符串"]
categories: ["算法"]
author: a东
---

##  反转字符串 II
给定一个字符串 s 和一个整数 k，从字符串开头算起，每计数至 2k 个字符，就反转这 2k 字符中的前 k 个字符。

- 如果剩余字符少于 k 个，则将剩余字符全部反转。
- 如果剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符，其余字符保持原样。
[leetcode 题目链接](https://leetcode-cn.com/problems/reverse-string-ii/)

示例1
```
输入：s = "abcdefg", k = 2
输出："bacdfeg"
```

示例2
```
输入：s = "abcd", k = 2
输出："bacd"
```
<!-- more -->

### 解题思路
题目要求每 `2k` 个字符翻转前 `k` 个，且末尾结束时根据剩余字符个数来决定具体的翻转规则。因此可以每次将指针移动 `2k` 个位置
```markdown
如果移动后剩余元素个数大于 `2k` 则翻转前 `k` 个并进入下一轮迭代
如果剩余元素个数小于 `2k` 但是大于 `k` 则翻转前 `k` 个并结束迭代
如果剩余元素个数小于 `k` 则翻转剩余的全部元素
```


```cgo
    func reverseStr(s string, k int) string {
        sbytes := []byte(s)
        for i := 0; i < len(sbytes); i += 2 * k {
            if len(sbytes[i:]) < k {  // 剩余元素个数小于 k 翻转剩余全部元素
                reverse(sbytes, i, len(sbytes) - 1)
            } else {
                sbytes = reverse(sbytes, i, i + k - 1) // 剩余元素个数大于 2k 或 在 (k,2k) 之间同样也翻转前 k 个元素
            }
        }
        return string(sbytes)
    }
    
    func reverse(sbytes []byte, start int, end int) []byte {
        for start < end {
            sbytes[start], sbytes[end] = sbytes[end], sbytes[start]
            start++
            end--
        }
        return sbytes
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是字符串长度。
- 空间复杂度：O(1)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/reverse-string-ii/solution/fan-zhuan-zi-fu-chuan-ii-by-leetcode-sol-ua7s/)






