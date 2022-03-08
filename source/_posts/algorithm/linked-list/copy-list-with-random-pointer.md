---
title: 复制带随机指针的链表
date: 2022-03-08
tags: ["链表"]
categories: ["算法"]
author: a东
---

## 复制带随机指针的链表
给你一个长度为 n 的链表，每个节点包含一个额外增加的随机指针 random ，该指针可以指向链表中的任何节点或空节点。

构造这个链表的 深拷贝。 深拷贝应该正好由 n 个 全新 节点组成，其中每个新节点的值都设为其对应的原节点的值。新节点的 next 指针和 random 指针也都应指向复制链表中的新节点，并使原链表和复制链表中的这些指针能够表示相同的链表状态。复制链表中的指针都不应指向原链表中的节点 。

例如，如果原链表中有 X 和 Y 两个节点，其中 X.random --> Y 。那么在复制链表中对应的两个节点 x 和 y ，同样有 x.random --> y 。

返回复制链表的头节点。

用一个由 n 个节点组成的链表来表示输入/输出中的链表。每个节点用一个 [val, random_index] 表示：

val：一个表示 Node.val 的整数。
random_index：随机指针指向的节点索引（范围从 0 到 n-1）；如果不指向任何节点，则为  null 。
你的代码 只 接受原链表的头节点 head 作为传入参数。
[ leetcode 题目链接](https://leetcode-cn.com/problems/copy-list-with-random-pointer/)

示例1
![链表](/images/algorithm/linked-list/random-list1.png)
```
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

示例2
![链表](/images/algorithm/linked-list/random-list2.png)
```
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```
<!-- more -->

示例3
![链表](/images/algorithm/linked-list/random-list3.png)
```
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
```

### 解题思路1
题目罗里吧嗦的说了一大堆，其实总结下来就是让我们深度拷贝一个链表，只不过这个链表相比普通的单链表多个一个随机指针，这个随机指针 `random` 随机指向链表中的任意节点或者为空。
既然如此我们不妨先看一下如何深度拷贝一个普通的单链表的处理过程：

```markdown
首先深度拷贝单链表的头结点
然后递归的深度拷贝后续节点，并在递归过程中维持链表建节点的连接关系
```
递归的结束条件是当遇到空的节点就可以结束了（空链表或到达链表末尾空节点）
```cgo
    type Node struct {
        Val  int
        Next *Node
    }
    
    func copyList(head *Node) *Node {
        return deepCopy(head)
    }
    
    func deepCopy(node *Node) *Node {
        if node == nil {
            return nil
        }
    
        copyNode := &Node{Val: node.Val}
        copyNode.Next = deepCopy(node.Next)
        return copyNode
    }
    
    func main() {
        // 构造链表
        vals := []int{5, 6, 7, 8, 9}
        var head *Node
        var curNode *Node
        for i, val := range vals {
            if i == 0 {
                head = &Node{Val: val}
                curNode = head
            } else {
                curNode.Next = &Node{Val: val}
                curNode = curNode.Next
            }
        }
        curNode.Next = nil
        // 打印链表
        curNode = head
        for curNode != nil {
            fmt.Println(curNode.Val)
            curNode = curNode.Next
        }
    }
```

有了上面深度拷贝单链表的处理过程我们再来看如何深度拷贝带随机指针的链表，首先可以肯定思路是和深度拷贝单链表一致的可以采用递归的方式处理。但是有一个问题，因为 `random` 指针的存在链表中可能出现环，如
`示例2` 中值为 `2` 的节点的 `random` 指针指向了自己，如果直接递归会导致无限循环递归直到内存溢出。因此可以使用一个 `hashtable` 记录每个节点被拷贝的情况（key 是原链表中节点，val 是对应的拷贝节点），每次拷贝前先查记录，如果已经被拷贝了则直接返回即可。



节点结构
```cgo
    type ListNode struct {
        Val  int
        Next *ListNode
        Random *Node
    }
```

遍历链表移除指定元素
```cgo
    var nodeMap = make(map[*Node]*Node)

    func copyRandomList(head *Node) *Node {
        return deepCopy(head)
    }
    
    func deepCopy(node *Node) *Node {
        if node == nil {
            return nil
        }
    
        if existNode, ok := nodeMap[node]; ok {
            return existNode
        }
    
        copyNode := &Node{Val:node.Val}
        nodeMap[node] = copyNode
        copyNode.Next = deepCopy(node.Next)
        copyNode.Random = deepCopy(node.Random)
        return copyNode
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是链表的长度。
- 空间复杂度：O(n)。


### 解题思路2
可以通过如下三步来进行复制
1. 在原链表的每一个节点后插入一个前一个节点的拷贝，完成 `Next` 拷贝
2. 为每个拷贝的节点关联 `Random`，很明显拷贝节点的 `Random` 就是它对应原节点 `Random` 的 `Next`
3. 将拷贝的链表从混合链表中拆解出来，只需要拆解 `Next`

![链表](/images/algorithm/linked-list/random-list.png)


```cgo
    func copyRandomList(head *Node) *Node {
        if head == nil {
            return nil
        }
    
        for node := head; node != nil; node = node.Next.Next {
            copyNode := &Node{Val: node.Val}
            copyNode.Next = node.Next
            node.Next = copyNode
        }
    
        for node := head; node != nil; node = node.Next.Next {
            if node.Random != nil {
                node.Next.Random = node.Random.Next
            }
        }
    
        dummyNode := &Node{Val: -1}
        curNode := dummyNode
        for node := head; node != nil; node = node.Next {
            copyNode := node.Next
            curNode.Next = copyNode
            curNode = curNode.Next
            node.Next = curNode.Next
        }
    
        return dummyNode.Next
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是链表的长度。
- 空间复杂度：O(1)。


## 参考
* [代码随想录](https://leetcode-cn.com/problems/copy-list-with-random-pointer/solution/fu-zhi-dai-sui-ji-zhi-zhen-de-lian-biao-rblsf/)





