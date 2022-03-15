---
title: 用队列实现栈
date: 2022-03-15
tags: ["栈&队列"]
categories: ["算法"]
author: a东
---

##  用队列实现栈
请你仅使用两个队列实现一个后入先出（LIFO）的栈，并支持普通栈的全部四种操作（push、top、pop 和 empty）。

实现 MyStack 类：

void push(int x) 将元素 x 压入栈顶。<br>
int pop() 移除并返回栈顶元素。<br>
int top() 返回栈顶元素。<br>
boolean empty() 如果栈是空的，返回 true ；否则，返回 false 。<br>

注意：<br>

你只能使用队列的基本操作 —— 也就是 push to back、peek/pop from front、size 和 is empty 这些操作。<br>
你所使用的语言也许不支持队列。 你可以使用 list （列表）或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。<br>
[leetcode 题目链接](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

示例1
```
输入：
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 2, 2, false]

解释：
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // 返回 2
myStack.pop(); // 返回 2
myStack.empty(); // 返回 False
```
<!-- more -->


### 解题思路
用数组模拟。

```cgo
    type MyStack struct {
        stack []int
    }
    
    func Constructor() MyStack {
        return MyStack{stack: make([]int, 0)}
    }
    
    
    func (this *MyStack) Push(x int)  {
        this.stack = append(this.stack, x)
    }
    
    
    func (this *MyStack) Pop() int {
        if len(this.stack) == 0 {
            return -1
        }
    
        val := this.stack[len(this.stack)-1]
        this.stack = this.stack[:len(this.stack)-1]
        return val
    }
    
    
    func (this *MyStack) Top() int {
        if len(this.stack) == 0 {
            return -1
        }
    
        return this.stack[len(this.stack)-1]
    }
    
    
    func (this *MyStack) Empty() bool {
        return len(this.stack) == 0
    }
```


### 复杂度分析
- 时间复杂度：O(1)。
- 空间复杂度：O(n)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/implement-stack-using-queues/solution/yong-dui-lie-shi-xian-zhan-by-leetcode-solution/)






