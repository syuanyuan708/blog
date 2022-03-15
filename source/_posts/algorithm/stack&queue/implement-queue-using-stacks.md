---
title: 用栈实现队列
date: 2022-03-15
tags: ["栈&队列"]
categories: ["算法"]
author: a东
---

##  用栈实现队列
请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（push、pop、peek、empty）：

实现 MyQueue 类：

void push(int x) 将元素 x 推到队列的末尾<br>
int pop() 从队列的开头移除并返回元素<br>
int peek() 返回队列开头的元素<br>
boolean empty() 如果队列为空，返回 true ；否则，返回 false<br>
说明：<br>

你只能使用标准的栈操作 —— 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可<br>
[leetcode 题目链接](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

示例1
```
输入：
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 1, 1, false]

解释：
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```
<!-- more -->


### 解题思路
用数组模拟。

```cgo
    type MyQueue struct {
        queue []int
    }
    
    
    func Constructor() MyQueue {
        return MyQueue{queue: make([]int, 0)}
    }
    
    
    func (this *MyQueue) Push(x int)  {
        this.queue = append(this.queue, x)
    }
    
    
    func (this *MyQueue) Pop() int {
        if len(this.queue) == 0 {
            return -1
        }
    
        val := this.queue[0]
        this.queue = this.queue[1:]
        return val
    }
    
    
    func (this *MyQueue) Peek() int {
        if len(this.queue) == 0 {
            return -1
        }
        return this.queue[0]
    }
    
    
    func (this *MyQueue) Empty() bool {
        return len(this.queue) == 0
    }
```


### 复杂度分析
- 时间复杂度：O(1)。
- 空间复杂度：O(n)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/implement-queue-using-stacks/solution/yong-zhan-shi-xian-dui-lie-by-leetcode/)






