---
title: 比较含退格的字符串
date: 2022-02-19
tags: ["数组"]
categories: ["算法"]
author: a东
---

## 比较含退格的字符串
给定 s 和 t 两个字符串，当它们分别被输入到空白的文本编辑器后，如果两者相等，返回 true 。# 代表退格字符。

注意：如果对空文本输入退格字符，文本继续为空。

[ leetcode 题目链接](https://leetcode-cn.com/problems/backspace-string-compare/)

示例1
```
输入：s = "ab#c", t = "ad#c"
输出：true
解释：s 和 t 都会变成 "ac"。
```

示例2
```
输入：s = "ab##", t = "c#d#"
输出：true
解释：s 和 t 都会变成 ""。
```
<!-- more -->

示例3
```
输入：s = "a#c", t = "b"
输出：false
解释：s 会变成 "c"，但 t 仍然是 "b"。
```

### 解题思路
类似的字符串比较问题都可以借助栈来进行处理，首先将字符串按照退格规格压入栈，若非退格符 `#` 则入栈，否则将栈顶元素出栈。

```cgo
    func buildStack(str string) []int32 {
        stack := []int32{}
        for _, c := range str {
            if c != '#' {
                stack = append(stack, c)
            } else {
                if len(stack) > 0 {
                    stack = stack[0:len(stack)-1]
                }
            }
        }
        return stack
    }
```

构造完栈后，对比2个栈中存储的退格后的字符串是否相同即可

```cgo
    func backspaceCompare(s string, t string) bool {
        stackS := buildStack(s)
        stackT := buildStack(t)
        if len(stackS) != len(stackT) {
            return false
        }
        for i := 0; i < len(stackS); i++ {
            if stackS[i] != stackT[i] {
                return false
            }
        }
        return true
    }
```

### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。




## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/backspace-string-compare/solution/bi-jiao-han-tui-ge-de-zi-fu-chuan-by-leetcode-solu/)






