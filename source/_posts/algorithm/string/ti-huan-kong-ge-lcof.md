---
title:  替换空格
date: 2022-03-12
tags: ["字符串"]
categories: ["算法"]
author: a东
---

##  替换空格
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

[leetcode 题目链接](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

示例1
```
输入：s = "We are happy."
输出："We%20are%20happy."
```

<!-- more -->

### 解题思路
遍历字符串并替换，或者先统计空格个数然后申请新空间后再填入替换后的新字符串。


```cgo
    func replaceSpace(s string) string {
        targetBytes := make([]byte, 0)
        for i := 0; i < len(s); i++ {
            if s[i] == byte(' ') {
                targetBytes = append(targetBytes, []byte{byte('%'), byte('2'), byte('0')}...)
            } else {
                targetBytes = append(targetBytes, s[i])
            }
        }
    
        return string(targetBytes)
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是字符串长度。
- 空间复杂度：O(1)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/solution/mian-shi-ti-05-ti-huan-kong-ge-by-leetcode-solutio/)






