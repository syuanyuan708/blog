---
title: 二叉树层序遍历
date: 2022-02-12
tags: ["二叉树"]
categories: ["算法"]
author: a东
---

## 二叉树层序遍历
给你二叉树的根节点 root ，返回其节点值的 层序遍历 。（即逐层地，从左到右访问所有节点）。
[ leetcode 题目链接](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)
![二叉树](/images/binary-tree-level-order-traversal/tree.jpeg)
<!-- more -->

示例1
```
输入：root = [3,9,20,null,null,15,7]
输出：[[3],[9,20],[15,7]]
```

示例2
```
输入：root = [1]
输出：[[1]]
```

示例3
```
输入：root = []
输出：[]
```

### 解题思路
我们首先来构造一棵二叉树，二叉树的存储方式主要分为链式存储和顺序存储，其中顺序存储是在算法处理中比较常用的一种。在顺序存储中，假设二叉树节点A在数组中的下标为 i , 那么有如下性质：

```
节点A的左子节点在数组中的下标：Index[A.Left]  = i*2+1
节点A的右子节点在数组中的下标：Index[A.Right] = i*2+2
```

那么我们可以得出一个根据节点值构造二叉树的过程如下：

**二叉树节点**
```go
    type TreeNode struct {
        Val   int
        Left  *TreeNode
        Right *TreeNode
    }
```

**构造二叉树**
```go
    func constructBinaryTree(values []int) *TreeNode {
        var root *TreeNode
        var treeNodes = make([]*TreeNode, len(values))
        // 根据各个节点的值构造节点数组
        for i, val := range values {
            var treeNode *TreeNode
            if val != -1 { // val等于 -1 代表空节点
                treeNode = &TreeNode{Val: val}
            }
            treeNodes[i] = treeNode
    
            if i == 0 {
                root = treeNode
            }
        }
        // 将各个节点根据节点下标计算公式进行关联，形成一棵树
        for i := 0; i*2+2 < len(treeNodes); i++ { // 边界条件，右节点下标不能超出数组长度
            if treeNodes[i] != nil {
                treeNodes[i].Left = treeNodes[i*2+1]
                treeNodes[i].Right = treeNodes[i*2+2]
            }
        }
    
        return root
    }
```

至此我们已经可以根据节点值的数组来构造一棵二叉树了，例如输入[4,1,6,0,2,5,7,-1,-1,-1,3,-1,-1,-1,8]构造二叉树如下：
![构造二叉树](/images/binary-tree-level-order-traversal/build-tree.png)

构造完二叉树后我们开始模拟每次遍历一层来层序遍历二叉树，每次遍历的过程都把当前层的值存储下来，遍历完后追加到结果集中。注意添加当前节点的左、右节点时做了判空处理，否则最后会多一层全空的数据。
**层序遍历二叉树**
```go
    func printBinaryTree(root *TreeNode) {
        var result = make([][]int, 0)
        var queue = make([]*TreeNode, 0)
        if root != nil {
            queue = append(queue, root)
        }
    
        for len(queue) > 0 {
            var level []int // 当前层的数据
            var size = len(queue) // 记录当前层节点个数
            for i := 0; i < size; i++ {
                if queue[i] != nil {
                    level = append(level, queue[i].Val)
                    queue = append(queue, queue[i].Left)
                    queue = append(queue, queue[i].Right)
                } else {
                    level = append(level, -1) // val等于 -1 代表空节点
                }
            }
            result = append(result, level)
            queue = queue[size:] // 向前推进
        }
    
        for i := 0; i < len(result); i++ { // 和 leetcode 原题要求稍有区别，如需要修改一下即可
            for j := 0; j < len(result[i]); j++ {
                fmt.Printf("%v ", result[i][j])
            }
            fmt.Println()
        }
    }
```


## 参考
* [代码随想录](https://programmercarl.com/%E5%89%8D%E5%BA%8F/ACM%E6%A8%A1%E5%BC%8F%E5%A6%82%E4%BD%95%E6%9E%84%E5%BB%BA%E4%BA%8C%E5%8F%89%E6%A0%91.html#java)






