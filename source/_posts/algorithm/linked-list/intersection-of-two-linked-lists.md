---
title: 链表相交
date: 2022-02-23
tags: ["链表"]
categories: ["算法"]
author: a东
mathjax: true
---

## 链表相交
给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。

[ leetcode 题目链接](https://leetcode-cn.com/problems/intersection-of-two-linked-lists-lcci/)

示例1
![链表](/images/algorithm/linked-list/intersection-of-two-linked-lists-1.png)
```
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Intersected at '8'
解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```
<!-- more -->

示例2
![链表](/images/algorithm/linked-list/intersection-of-two-linked-lists-2.png)
```
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Intersected at '2'
解释：相交节点的值为 2 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
```

示例3
![链表](/images/algorithm/linked-list/intersection-of-two-linked-lists-3.png)
```
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。
由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
这两个链表不相交，因此返回 null 。
```

### 解题思路
基本思路是先找平2个链表的长度差，然后让2个链表同步向前移动直到结束。我们让`curA` 从 `A` 链表开始，`curB` 从 `B` 链表开始，遍历一遍后得到2个链表的长度 `lenA` 和 `lenB`。然后长的链表先移动
`abs(lenA-lenB)` 步，最后2个指针再同步移动直到他们指向同一个节点为止。如果有相交节点一定会有 `curA == curB` ，如果没有相交节点则最后2个指针都指向各自链表末尾的空节点也满足 `curA == curB`。

#### 这样最终的结果一定是 `curA == curB` 存在如下2种情况：
- `curA == curB` 且节点不为空，2个链表有相交节点
- `curA == curB` 且节点为空，2个链表没有相交节点


节点结构
```cgo
    type ListNode struct {
        Val  int
        Next *ListNode
    }
```

交换链表节点
```cgo
    func getIntersectionNode(headA, headB *ListNode) *ListNode {
        curA := headA
        curB := headB
        lenA, lenB := 0, 0
        for curA != nil {
            curA = curA.Next
            lenA++
        }
        for curB != nil {
            curB = curB.Next
            lenB++
        }
    
        curA, curB = headA, headB
        if lenA > lenB {
            for i := 0; i < lenA - lenB; i++ {
                curA = curA.Next
            }
        } else {
            for i := 0; i < lenB - lenA; i++ {
                curB = curB.Next
            }
        }
    
        for curA != curB {
            curA = curA.Next
            curB = curB.Next
        }
        return curA
    }
```


### 复杂度分析
- 时间复杂度：O(n+m)，2个链表的长度和。
- 空间复杂度：O(1)。



## 参考
* [代码随想录](https://www.programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html#%E6%80%9D%E8%B7%AF)






