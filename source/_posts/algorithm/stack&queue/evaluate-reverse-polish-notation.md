---
title: 逆波兰表达式求值
date: 2022-03-15
tags: ["栈&队列"]
categories: ["算法"]
author: a东
---

##  逆波兰表达式求值
根据 逆波兰表示法，求表达式的值。

有效的算符包括 +、-、*、/ 。每个运算对象可以是整数，也可以是另一个逆波兰表达式。

注意 两个整数之间的除法只保留整数部分。

可以保证给定的逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

[leetcode 题目链接](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/)

示例1
```
输入：tokens = ["2","1","+","3","*"]
输出：9
解释：该算式转化为常见的中缀算术表达式为：((2 + 1) * 3) = 9
```

示例2
```
输入：tokens = ["4","13","5","/","+"]
输出：6
解释：该算式转化为常见的中缀算术表达式为：(4 + (13 / 5)) = 6
```
<!-- more -->

示例3
```
输入：tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
输出：22
解释：该算式转化为常见的中缀算术表达式为：
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```


### 解题思路
借助栈进行处理，遍历数组如果当前元素不是 `+、-、*、/` 中任何一个则入栈，如果是运算符中的任何一个则弹出栈顶的前 2 个元素并根据运算符计算值，然后将计算所得值压入栈中。
需要注意的一点是运算时 2 个参数的前后顺序是 `栈顶的第 2 个元素 compute 栈顶的第 1 个元素` 。

```cgo
    func evalRPN(tokens []string) int {
        stack := make([]int, 0)
        tokenMap := map[string]func(num1 int, num2 int) int{
            `+`: func(num1 int, num2 int) int { return num1 + num2 },
            `-`: func(num1 int, num2 int) int { return num1 - num2 },
            `*`: func(num1 int, num2 int) int { return num1 * num2 },
            `/`: func(num1 int, num2 int) int { return num1 / num2 },
        }
    
        for _, token := range tokens {
            if len(stack) == 0 || tokenMap[token] == nil {
                num, _ := strconv.Atoi(token)
                stack = append(stack, num)
            } else {
                result := tokenMap[token](stack[len(stack)-2], stack[len(stack)-1])
                stack = stack[:len(stack)-2]
                stack = append(stack, result)
            }
        }
        return stack[0]
    }
```


### 复杂度分析
- 时间复杂度：O(n)，n 是数组长度。
- 空间复杂度：O(n)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/solution/ni-bo-lan-biao-da-shi-qiu-zhi-by-leetcod-wue9/)






