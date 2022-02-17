---
title: 在排序数组中查找元素的第一个和最后一个位置
date: 2022-02-17
tags: ["二分法"]
categories: ["算法"]
author: a东
---

## 在排序数组中查找元素的第一个和最后一个位置
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。
如果数组中不存在目标值 target，返回 [-1, -1]。`nums 是一个非递减数组`
[ leetcode 题目链接](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

示例1
```
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
```

示例2
```
输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]
```
<!-- more -->


示例3
```
输入：nums = [], target = 0
输出：[-1,-1]
```

### 解题思路
#### 暴力求解法
只需要一次遍历即可，在此不做讨论。

#### 二分查找法
因为数组是非递减的可以考虑使用二分查找分别查找目标值在数组中的左边界 `leftBorder` 和右边界 `rightBorder` 。

**查找左边界**
```cgo
    func searchLeftBorder(nums []int, target int) int {
        left := 0
        right := len(nums) - 1
        leftBorder := -1
        for left <= right {
            mid := left + (right-left)/2
            if nums[mid] == target {
                leftBorder = mid // 记录左边界
                right = mid - 1  // 向左侧查找更左的边界
            } else if nums[mid] < target {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
        return leftBorder
    }
```

**查找右边界**
```cgo
    func searchRightBorder(nums []int, target int) int {
        left := 0
        right := len(nums) - 1
        rightBorder := -1
        for left <= right {
            mid := left + (right-left)/2
            if nums[mid] == target {
                rightBorder = mid  // 记录右边界
                left = mid + 1     // 向右侧查找更右的边界
            } else if nums[mid] < target {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
        return rightBorder
    }
```
上面的查找过程和标准的二分查找算法区别主要在于，一旦查找到目标值则更新边界值，并且向左查找更左的边界或向右查找更右的边界。查找完左右边界则最终处理结果如下：
```cgo
    func searchRange(nums []int, target int) []int {
        leftBorder := searchLeftBorder(nums, target)
        rightBorder := searchRightBorder(nums, target)
        return []int{leftBorder, rightBorder}
    }
```

**复杂度分析**
- 时间复杂度：O(log n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。




## 参考
* [代码随想录](https://programmercarl.com/0034.%E5%9C%A8%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E6%9F%A5%E6%89%BE%E5%85%83%E7%B4%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%92%8C%E6%9C%80%E5%90%8E%E4%B8%80%E4%B8%AA%E4%BD%8D%E7%BD%AE.html)
* [leetcode 题解](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/solution/zai-pai-xu-shu-zu-zhong-cha-zhao-yuan-su-de-di-3-4/)






