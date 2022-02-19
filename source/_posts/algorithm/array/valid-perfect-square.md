---
title: 有效的完全平方数
date: 2022-02-17
tags: ["数组", "二分法"]
categories: ["算法"]
author: a东
---

## 有效的完全平方数
给定一个 正整数 num ，编写一个函数，如果 num 是一个完全平方数，则返回 true ，否则返回 false 。

[ leetcode 题目链接](https://leetcode-cn.com/problems/valid-perfect-square/)

示例1
```
输入：num = 16
输出：true  
```

示例2
```
输入：num = 14
输出：false   
```
<!-- more -->

### 解题思路
题目和求平方根类似，因此可以把问题转化为在一个 `[1,n]` 的升序数组中查找一个满足条件的平方根值。根据数组的特性 **有序**、**无重复元素**，可以直接采用二分查找算法求解。
因为 `n` 的平方根不会超过 `n/2 + 1` 因此右边界可以直接设为 `n/2 + 1`

```cgo
    func isPerfectSquare(num int) bool {
        left := 0
        right := num/2 + 1
        for left <= right {
            mid := left + (right - left) / 2
            if mid * mid == num {
                return true
            } else if mid * mid < num {
                left = mid +1
            } else {
                right = mid - 1
            }
        }
        return false
    }
```


### 复杂度分析
- 时间复杂度：O(log n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。

## 参考
* [leetcode](https://leetcode-cn.com/problems/valid-perfect-square/)






