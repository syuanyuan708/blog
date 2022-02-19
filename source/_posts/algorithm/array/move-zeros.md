---
title: 移动零
date: 2022-02-19
tags: ["数组"]
categories: ["算法"]
author: a东
---

## 移动零
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

请注意 ，必须在不复制数组的情况下原地对数组进行操作。

[ leetcode 题目链接](https://leetcode-cn.com/problems/move-zeroes/)

示例1
```
输入: nums = [0,1,0,3,12]
输出: [1,3,12,0,0] 
```

示例2
```
输入: nums = [0]
输出: [0]
```
<!-- more -->


### 解题思路
#### 双指针法
依然采用双指针，`slow` 标记每次放置非0元素的位置，`fast` 指针依次向后遍历数组。每次遇到非0的元素则把 `slow` 和 `fast` 交换，这样遍历完后所有0都被移到数组尾端。

```cgo
    func moveZeroes(nums []int)  {
        slow := 0
        fast := 0
        for ; fast < len(nums); fast++ {
            if nums[fast] != 0 {
                nums[slow], nums[fast] = nums[fast], nums[slow]
                slow++
            }
        }
    }
```
### 复杂度分析
- 时间复杂度：O(log n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。




## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/solution/shan-chu-pai-xu-shu-zu-zhong-de-zhong-fu-tudo/)






