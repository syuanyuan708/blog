---
title: 螺旋矩阵 II
date: 2022-02-20
tags: ["数组"]
categories: ["算法"]
author: a东
mathjax: true
---

## 螺旋矩阵 II
给你一个正整数 n ，生成一个包含 1 到 $n^2$ 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

[ leetcode 题目链接](https://leetcode-cn.com/problems/spiral-matrix-ii/)

示例1
![矩阵](/images/algorithm/array/matrix.png)
```
输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
```

示例2
```
输入：n = 1
输出：[[1]]
```
<!-- more -->

### 解题思路
模拟操作，从左至右、从上至下、从右至左、从下至上依次循环填入数字到矩阵中，采用 `num` 迭代要插入的值。


```cgo
    func generateMatrix(n int) [][]int {
        var top, buttom = 0, n - 1
        var left, right = 0, n - 1
        var result = make([][]int, n)
        for i := 0; i < n; i++ {
            result[i] = make([]int, n)
        }
    
        var num = 1
        for num <= n * n {
            for i := left; i <= right; i++ {
                result[top][i] = num
                num++
            }
            top++
    
            for i := top; i <= buttom; i++ {
                result[i][right] = num
                num++
            }
            right--
    
            for i := right; i >= left; i-- {
                result[buttom][i] = num
                num++
            }
            buttom--
    
            for i := buttom; i >= top; i-- {
                result[i][left] = num
                num++
            }
            left++
        }
        return result
    }
```

### 复杂度分析
- 时间复杂度：$O(n^2)$。
- 空间复杂度：$O(n^2)$。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/spiral-matrix-ii/solution/luo-xuan-ju-zhen-ii-by-leetcode-solution-f7fp/)






