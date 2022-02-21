---
title: 移除链表元素
date: 2022-02-19
tags: ["链表"]
categories: ["算法"]
author: a东
---

## 移除链表元素
给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 新的头节点 。

[ leetcode 题目链接](https://leetcode-cn.com/problems/remove-linked-list-elements/)

示例1
![链表](/images/algorithm/linked-list/remove-linked-list-elements.png)
```
输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]
```

示例2
```
输入：head = [], val = 1
输出：[]
```
<!-- more -->

示例3
```
输入：head = [7,7,7,7], val = 7
输出：[]
```

### 解题思路
在链表中移除一个元素的操作 `cur.Next = cur.Next.Next` 即可，如 `示例1` 中要移除第3个值为6的元素时 `cur` 应该指向第2个值为2的元素。因此移除一个元素 `X` 需要
获取 `X` 的前一个元素，由于有可能需要移除头结点元素因此可以借助一个虚拟节点来处理边界条件。

节点结构
```cgo
    type ListNode struct {
        Val  int
        Next *ListNode
    }
```

遍历链表移除指定元素
```cgo
    func removeElements(head *ListNode, val int) *ListNode {
        dummy := &ListNode{Next: head} // 虚拟头结点
        for cur := dummy; cur.Next != nil; { // cur.Next == nil 时遍历完整个链表
            if cur.Next.Val == val {
                cur.Next = cur.Next.Next
            } else {
                cur = cur.Next
            }
        }
        return dummy.Next
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。



## 参考
* [代码随想录](https://www.programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)
* [leetcode 题解](https://leetcode-cn.com/problems/remove-linked-list-elements/solution/yi-chu-lian-biao-yuan-su-by-leetcode-sol-654m/)






