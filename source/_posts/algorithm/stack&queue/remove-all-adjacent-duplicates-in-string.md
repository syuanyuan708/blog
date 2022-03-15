---
title: 删除字符串中的所有相邻重复项
date: 2022-03-15
tags: ["栈&队列"]
categories: ["算法"]
author: a东
---

##  删除字符串中的所有相邻重复项
给出由小写字母组成的字符串 S，重复项删除操作会选择两个相邻且相同的字母，并删除它们。

在 S 上反复执行重复项删除操作，直到无法继续删除。

在完成所有重复项删除操作后返回最终的字符串。答案保证唯一。

[leetcode 题目链接](https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/)

示例1
```
输入："abbaca"
输出："ca"
解释：
例如，在 "abbaca" 中，我们可以删除 "bb" 由于两字母相邻且相同，这是此时唯一可以执行删除操作的重复项。之后我们得到字符串 "aaca"，其中又只有 "aa" 可以执行重复项删除操作，所以最后的字符串为 "ca"。
```

<!-- more -->


### 解题思路
和有效括号的处理方式一样也是借助栈，只是判断元素是否出栈的条件改为当前元素与栈顶元素是否相同，相同则出栈，不相同则入栈。

```cgo
    func removeDuplicates(s string) string {
        stack := make([]byte, 0)
        for i := 0; i < len(s); i++ {
            if len(stack) == 0 || stack[len(stack) - 1] != s[i] {
                stack = append(stack, s[i])
            } else {
                stack = stack[:len(stack) - 1]
            }
        }
    
        return string(stack)
    }
```


### 复杂度分析
- 时间复杂度：O(n)，n 是字符串长度。
- 空间复杂度：O(n)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/solution/shan-chu-zi-fu-chuan-zhong-de-suo-you-xi-4ohr/)






