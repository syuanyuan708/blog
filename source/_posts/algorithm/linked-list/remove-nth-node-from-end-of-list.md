---
title: 删除链表的倒数第 N 个节点
date: 2022-02-22
tags: ["链表"]
categories: ["算法"]
author: a东
mathjax: true
---

## 删除链表的倒数第 N 个节点
给你一个链表，删除链表的倒数第 n 个节点，并且返回链表的头节点。

[ leetcode 题目链接](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

示例1
![链表](/images/algorithm/linked-list/remove-nth-node-exam.png)
```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```
<!-- more -->

示例2
```
输入：head = [1], n = 1
输出：[]
```

示例3
```
输入：head = [1,2], n = 1
输出：[1]
```

### 解题思路
在链表中删除一个节点 `A` 的操作为 `A.Next = A.Next.Next` 因此要删除 `A` 节点，需要找到 `A` 的前驱节点。因为有可能会删除头节点，因此为了便于处理引入一个虚拟头节点 `dummy` 。
假设要删除倒数第 `x` 个节点，实际就是要找到它的前缀节点也就是倒数第 `x+1` 个节点。这个问题可以采用双指针来解决，初始 `slow`、`fast` 都指向虚拟头节点。

#### 处理过程如下
- 第一步先让 `fast` 指针向前移动 `x+1` 次。
- 第二步`slow` 和 `fast` 同时移动直到 `fast` 指向 `nil`。假设节点个数为 `n` ，则第二步中 `fast` 指针共移动了 `(n+1) - (x+1) = n-x` 步，因此 `slow` 也移动了 `n-x` 步。
  
此时 `slow` 指向的位置为 `n-x` 也就是链表的倒数第 `x+1` 个节点 （倒数第 `x` 个节点的前驱），因此执行 `slow.Next = slow.Next.Next` 完成删除节点的操作即可。


![处理过程](/images/algorithm/linked-list/remove-nth-node-step.png)

节点结构
```cgo
    type ListNode struct {
        Val  int
        Next *ListNode
    }
```

交换链表节点
```cgo
    func removeNthFromEnd(head *ListNode, n int) *ListNode {
        dummy := &ListNode{Val: -1, Next: head}
        fast := dummy
        for i := 0; i <= n; i++ {
            fast = fast.Next
        }
    
        slow := dummy
        for fast != nil {
            fast = fast.Next
            slow = slow.Next
        }
    
        slow.Next = slow.Next.Next
        return dummy.Next
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/solution/shan-chu-lian-biao-de-dao-shu-di-nge-jie-dian-b-61/)






