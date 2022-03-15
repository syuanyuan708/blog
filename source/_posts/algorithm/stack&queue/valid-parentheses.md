---
title: 有效的括号
date: 2022-03-15
tags: ["栈&队列"]
categories: ["算法"]
author: a东
---

##  有效的括号
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。<br>
左括号必须以正确的顺序闭合。<br>

[leetcode 题目链接](https://leetcode-cn.com/problems/valid-parentheses/)

示例1
```
输入：s = "()"
输出：true
```

示例2
```
输入：s = "()[]{}"
输出：true
```
<!-- more -->

示例3
```
输入：s = "(]"
输出：false
```

示例4
```
输入：s = "([)]"
输出：false
```

示例5
```
输入：s = "{[]}"
输出：true
```

### 解题思路
使用栈进行处理，遍历字符串如果栈为空或当前字符不是右括号 `)、]、}` 中的任何一个则压入栈中，如果是右括号中的任一个且与栈顶括号能匹配成一对则将栈顶元素出栈，最后如果字符串有效则栈的长度必然为 0 。

```cgo
    func isValid(s string) bool {
        stack := make([]rune, 0)
        chMap := map[rune]rune {
            '(': ')',
            '[': ']',
            '{': '}',
        }
    
        for _, ch := range s {
            if len(stack) == 0 || chMap[stack[len(stack) - 1]] != ch {
                stack = append(stack, ch)
            } else {
                stack = stack[:len(stack) - 1]
            }
        }
        return len(stack) == 0
    }
```


### 复杂度分析
- 时间复杂度：O(n)，n 是字符串长度。
- 空间复杂度：O(n)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/valid-parentheses/solution/you-xiao-de-gua-hao-by-leetcode-solution/)






