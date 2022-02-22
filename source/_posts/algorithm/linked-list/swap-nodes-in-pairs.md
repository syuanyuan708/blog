---
title: 两两交换链表中的节点
date: 2022-02-22
tags: ["链表"]
categories: ["算法"]
author: a东
mathjax: true
---

## 两两交换链表中的节点
给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

[ leetcode 题目链接](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

示例1
![链表](/images/algorithm/linked-list/swap-nodes-in-pairs.png)
```
输入：head = [1,2,3,4]
输出：[2,1,4,3]
```
<!-- more -->

示例2
```
输入：head = []
输出：[]
```

示例3
```
输入：head = [1]
输出：[1]
```

### 解题思路
题目要求将链表中的节点2个一对进行交换，如 `示例1` 原链表为 `1-2-3-4` 交换后的结果为 `2-1-4-3`。可以看到交换完以后头节点发生了改变，因此为了方便处理我们可以引入一个虚拟头节点 `dummyHead` 指向原链表的头节点 `head`。
接下来我们需要交换 `dummyHead` 节点后的2个节点 `node1 = dummyHead.Next`、`node2 = dummyHead.Next.Next`，并在交换完成后将 `dummyHead` 指向 `node1` 来继续处理后续的节点对。由于我们最后需要返回 `dummyHead.Next` 
做为新链表的头节点，因此需要一个临时节点 `cursor = dummyHead` 代替 `dummyHead` 来进行迭代遍历。这里有一个点要注意就是节点之间链接的顺序，如下这种链接是错误的因为会一次交换后会丢失 `node2` 的原后继节点。
![错误步骤](/images/algorithm/linked-list/swap-nodes-error-exam.png)

因此正确的交换步骤如下
![错误步骤](/images/algorithm/linked-list/swap-nodes-exam.png)

边界条件为 `cursor.Next == nil` (后面只剩一个节点) 或 `cursor.Next.Next == nil`（后续没有节点）

节点结构
```cgo
    type ListNode struct {
        Val  int
        Next *ListNode
    }
```

交换链表节点
```cgo
    func swapPairs(head *ListNode) *ListNode {
        dummyHead := &ListNode{Val: -1, Next: head}
        cursor := dummyHead
        for cursor.Next != nil && cursor.Next.Next != nil {
            node1, node2 := cursor.Next, cursor.Next.Next
            cursor.Next = node2
            node1.Next = node2.Next
            node2.Next = node1
            cursor = node1
        }
        return dummyHead.Next
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/swap-nodes-in-pairs/solution/liang-liang-jiao-huan-lian-biao-zhong-de-jie-di-91/)






