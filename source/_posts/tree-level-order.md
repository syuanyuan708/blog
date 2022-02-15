---
title: 二叉树层序遍历
date: 2022-02-12
tags: ["二叉树"]
categories: ["算法"]
author: a东
---

## 二叉树层序遍历
给你二叉树的根节点 root ，返回其节点值的 层序遍历 。（即逐层地，从左到右访问所有节点）。[leetcode题目链接](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)
![二叉树](/images/tree-level-order/tree.jpeg)
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

思路

二叉树的层序遍历是一道比较符合人的逻辑思维推导的一道题，主要考察的是我们的代码模拟能力和对二叉树特性的一些理解。
首先二叉树的存储方式主要分为链式存储和顺序存储，而顺序存储又是在算法处理中比较常用的一种。在顺序存储中，假设二叉树的节点A在数组中的下标为 i , 那么有如下性质：

```
Index[A.Left] = i*2+1
Index[A.Right] = i*2+2
```

那么我们可以得出一个根据节点值构造二叉树的过程如下

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
        
        for i, val := range values {
            var treeNode *TreeNode
            if val != -1 {
                treeNode = &TreeNode{Val: val}
            }
            treeNodes[i] = treeNode
    
            if i == 0 {
                root = treeNode
            }
        }
    
        for i := 0; i*2+2 < len(treeNodes); i++ {
            if treeNodes[i] != nil {
                treeNodes[i].Left = treeNodes[i*2+1]
                treeNodes[i].Right = treeNodes[i*2+2]
            }
        }
    
        return root
    }
```


构造完二叉树后我们开始模拟每次遍历一层来层序遍历二叉树，每次遍历的过程都把当前层的值存储下来，遍历完后追加到结果集中。注意添加当前节点的左、右节点时做了判空处理，否则最后会多一层全空的数据。

```go
    func printBinaryTree(root *TreeNode) {
        var result = make([][]int, 0)
        var queue = make([]*TreeNode, 0)
        if root != nil {
            queue = append(queue, root)
        }
    
        for len(queue) > 0 {
            var level []int
            var size = len(queue)
            for i := 0; i < size; i++ {
                if queue[i] != nil {
                    level = append(level, queue[i].Val)
                    queue = append(queue, queue[i].Left)
                    queue = append(queue, queue[i].Right)
                } else {
                    level = append(level, -1)
                }
            }
            result = append(result, level)
            queue = queue[size:]
        }
    
        for i := 0; i < len(result); i++ {
            for j := 0; j < len(result[i]); j++ {
                fmt.Printf("%v ", result[i][j])
            }
            fmt.Println()
        }
    }
```


## 参考
* [代码随想录](https://programmercarl.com/)






