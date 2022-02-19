---
title: 有序数组的平方
date: 2022-02-19
tags: ["数组"]
categories: ["算法"]
author: a东
---

## 有序数组的平方
给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

[ leetcode 题目链接](https://leetcode-cn.com/problems/move-zeroes/)

示例1
```
输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]，排序后，数组变为 [0,1,9,16,100]
```

示例2
```
输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]
```
<!-- more -->


### 解题思路
因为数组是有序的，且可能存在负数则平方后负数的平方值可能被放大成为最大元素，所以平方的最大值为第一个元素的平方或最后一个元素的平方，同理可以求得第二大的平方数。因此我们采用从数组两端逼近的方式每次求剩余数组中平方最大的值，然后压入结果数组的尾端。

```cgo
    func sortedSquares(nums []int) []int {
        left := 0
        right := len(nums) - 1
        cur := len(nums) - 1
        res := make([]int, len(nums))
        for left <= right {
            if nums[left] * nums[left] >= nums[right] * nums[right] {
                res[cur] = nums[left] * nums[left]
                left = left + 1
            } else {
                res[cur] =  nums[right] * nums[right]
                right = right - 1
            }
            cur = cur - 1
        }
        return res
    }
```
### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。




## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/squares-of-a-sorted-array/solution/you-xu-shu-zu-de-ping-fang-by-leetcode-solution/)






