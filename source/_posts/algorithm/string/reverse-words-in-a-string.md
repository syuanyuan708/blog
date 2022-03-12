---
title:  翻转字符串里的单词
date: 2022-03-12
tags: ["字符串"]
categories: ["算法"]
author: a东
---

##  翻转字符串里的单词
给你一个字符串 s ，逐个翻转字符串中的所有 单词 。

单词 是由非空格字符组成的字符串。s 中使用至少一个空格将字符串中的 单词 分隔开。

请你返回一个翻转 s 中单词顺序并用单个空格相连的字符串。

说明：
输入字符串 s 可以在前面、后面或者单词间包含多余的空格。
翻转后单词间应当仅用一个空格分隔。
翻转后的字符串中不应包含额外的空格。
[leetcode 题目链接](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

示例1
```
输入：s = "the sky is blue"
输出："blue is sky the"
```

示例2
```
输入：s = "  hello world  "
输出："world hello"
解释：输入字符串可以在前面或者后面包含多余的空格，但是翻转后的字符不能包括。
```
<!-- more -->

示例3
```
输入：s = "a good   example"
输出："example good a"
解释：如果两个单词间有多余的空格，将翻转后单词间的空格减少到只含一个。
```

示例4
```
输入：s = "  Bob    Loves  Alice   "
输出："Alice Loves Bob"
```

### 解题思路
题目需要对字符串进行按单词翻转处理并设计到对空格的处理，可以按如下步骤处理
```markdown
先分别从字符串的首尾进行扫描处理，去除字符串首尾的空格，trim
接着遍历上一步处理所得的字符串，将单词之间的多个空格缩减为一个
然后将整个字符串进行翻转
最后按单词进行翻转
```


```cgo
    func reverseWords(s string) string {
        start, end := 0, len(s) - 1
        for i := 0; i < len(s); i++ { // trim 字符串首
            if s[i] != byte(' ') {
                break
            }
            start++
        }
    
        for j := len(s) - 1; j >= 0; j-- { // trim 字符串尾
            if s[j] != byte(' ') {
                break
            }
            end--
        }
    
        sbytes := make([]byte, 0)
        for i := start; i <= end;  { // 多个空格变一个空格
            if s[i] != byte(' ') {
                sbytes = append(sbytes, s[i])
                i++
            } else {
                for s[i] == byte(' ') {
                    i++
                }
                sbytes = append(sbytes, byte(' '))
            }
        }
    
        sbytes = reverse(sbytes, 0, len(sbytes) - 1) // 翻转字符串
    
        start = 0
        for i := 0; i < len(sbytes); i++ { // 翻转单词
            if sbytes[i] == byte(' ') {
                reverse(sbytes, start, i - 1)
                start = i + 1
            }
    
            if i == len(sbytes) - 1 { // 末尾单词也需要翻转
                reverse(sbytes, start, i)
            }
        }
        return string(sbytes)
    }
    
    func reverse(sbytes []byte, left int, right int) []byte {
        for left < right {
            sbytes[left], sbytes[right] = sbytes[right], sbytes[left]
            left++
            right--
        }
        return sbytes
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是字符串长度。
- 空间复杂度：O(n)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/reverse-words-in-a-string/solution/fan-zhuan-zi-fu-chuan-li-de-dan-ci-by-leetcode-sol/)






