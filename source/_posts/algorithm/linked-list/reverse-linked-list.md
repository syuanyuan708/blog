---
title: 反转链表
date: 2022-02-21
tags: ["链表"]
categories: ["算法"]
author: a东
---

## 反转链表
给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

[ leetcode 题目链接](https://leetcode-cn.com/problems/reverse-linked-list/)

示例1
![链表](/images/algorithm/linked-list/reverse-1.png)
```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```
<!-- more -->

示例2
![链表](/images/algorithm/linked-list/reverse-2.png)
```
输入：head = [1,2]
输出：[2,1]
```

示例3
```
输入：head = []
输出：[]
```

### 解题思路
翻转链表是链表处理中的一个常见问题，那么如何对链表进行翻转呢？首先翻转后原头结点 `head` 应该指向一个空节点，因此需要借助一个虚拟头结点。此外每次翻转将当前节点的 `next` 指向它的前一个节点后会丢失当前节点的下一个节点，因此需要一个后继节点
记录当前节点的下一个节点以便继续翻转后续的节点。

节点结构
```cgo
    type ListNode struct {
        Val  int
        Next *ListNode
    }
```

翻转链表
```cgo
    func reverseList(head *ListNode) *ListNode {
        var p *ListNode
        q := head
        for q != nil {
            r := q.Next
            q.Next = p
            p = q
            q = r
        }
        return p
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/reverse-linked-list/solution/fan-zhuan-lian-biao-by-leetcode-solution-d1k2/)






