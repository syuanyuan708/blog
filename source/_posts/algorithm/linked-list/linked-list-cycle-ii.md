---
title: 环形链表 II
date: 2022-02-22
tags: ["链表"]
categories: ["算法"]
author: a东
mathjax: true
---

## 环形链表 II
给定一个链表的头节点  head ，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

[ leetcode 题目链接](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

示例1
![链表](/images/algorithm/linked-list/linked-list-cycle-ii-1.png)
```
输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点。
```
<!-- more -->

示例2
![链表](/images/algorithm/linked-list/linked-list-cycle-ii-2.png)
```
输入：head = [1,2], pos = 0
输出：返回索引为 0 的链表节点
解释：链表中有一个环，其尾部连接到第一个节点。
```

示例3
![链表](/images/algorithm/linked-list/linked-list-cycle-ii-3.png)
```
输入：head = [1], pos = -1
输出：返回 null
解释：链表中没有环。
```

### 解题思路
处理过程主要分2部分，1是确定链表是否有环、2是如果有环如何找到入口。先说如何确定链表是否有环，使用 `slow`、`fast` 2个指针 `slow` 每次向前移动1步 `fast` 每次向前移动2步，如果链表有环那么2个指针一定会相遇。
如下图因为 `fast` 比 `slow` 移动快，则最终 `fast` 会追赶上 `slow` 此时或者恰好赶上2指针相遇，或者 `fast` 在 `slow` 后面一个位置，下一步移动也会相遇。 

![判断有环](/images/algorithm/linked-list/linked-list-cycle-step1.png)

确定有环之后寻找环的入口，如下图可以得到下列数学关系
```markdown
x + y + m*(y + z) = 2(x + y + n*(y + z))
(m - 2n)*(y + z) = x + y
x = (m - 2n -1)*(y + z) + y
```
根据上面的数学关系3可知，从链表头节点到环形入口节点的距离 `x` 等于 `(m -2n -1)` 圈再加上环形入口到 `slow`、`fast` 相遇处的距离。因此 `slow` 和 `fast` 相遇后 `slow` 重新指向链表头节点然后 `slow`、`fast` 同时每次移动一步，当再次相遇时即在环形入口节点处。

![寻找入口](/images/algorithm/linked-list/linked-list-cycle-step2.png)

节点结构
```cgo
    type ListNode struct {
        Val  int
        Next *ListNode
    }
```

寻找环的入口
```cgo
    func detectCycle(head *ListNode) *ListNode {
        slow := head
        fast := head
        for slow != nil && fast != nil && fast.Next != nil {
            slow= slow.Next
            fast = fast.Next.Next
            if slow == fast {
                break
            }
        }
    
        if slow == nil || fast == nil || fast.Next == nil {
            return nil
        }
    
        slow = head
        for slow != fast {
            slow = slow.Next
            fast = fast.Next
        }
        return slow
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/linked-list-cycle-ii/solution/huan-xing-lian-biao-ii-by-leetcode-solution/)
* [代码随想录](https://www.programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html#%E6%80%9D%E8%B7%AF)






