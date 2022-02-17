---
title: 搜索插入位置
date: 2022-02-17
tags: ["二分法"]
categories: ["算法"]
author: a东
---

## 搜索插入位置
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。`nums 为无重复元素的升序排列数组`

请必须使用时间复杂度为 O(log n) 的算法。

[ leetcode 题目链接](https://leetcode-cn.com/problems/binary-search/)

示例1
```
输入: nums = [1,3,5,6], target = 5
输出: 2   
```

示例2
```
输入: nums = [1,3,5,6], target = 2
输出: 1 
```
<!-- more -->


示例3
```
输入: nums = [1,3,5,6], target = 7
输出: 4
```


示例4
```
输入: nums = [1,3,5,6], target = 0
输出: 0 
```


示例5
```
输入: nums = [1], target = 0
输出: 0
```

### 题解思路
#### 暴力求解法
虽然题目要求使用O(log n)时间复杂度的算法，但是O(n)时间复杂度在 `leetcode` 上也是可以通过的，我们先来看一下暴力求解法
我们分析一下目标值可能的集中情况：
1. 目标值在数组内，对于这种情况只需要查找到它的位置并返回即可
2. 目标值不在数组内，这种情况需要返回它被按顺序插入的位置，比如**`示例2`**所示。这种又分3种情况
    2.1 目标值 > 数组最小值 && 目标值 < 数组最大值
    2.2 目标值 < 数组最小值
    2.3 目标值 > 数组最大值
 
考虑清楚上面可能出现的几种情况，就可以开始写代码了
```go
    func searchInsert(nums []int, target int) int {
        for i := 0; i < len(nums); i++ {
            if nums[i] >= target { // 找到插入位置，包含了 1、2.1、2.2 三种 case
                return i
            }
        }
        return len(nums) // 目标值大于数组中最大值，对应 2.3 的 case
    }
```

**复杂度分析**
- 时间复杂度：O(n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。

#### 二分查找法
数组是无重复元素的升序数组，因此可以使用二分查找算法。还是针对上面分析所得的集中可能存在的情况，若目标值在数组中则根据二分查找法可以找到对应的位置并返回。若目标值不在数组内呢?
在前一篇介绍二分查找算法的文章 [二分查找算法](/2022/02/15/binary-search/) 中我们分析了如果被查找目标值不在数组内，最终结束查找后的 `left` 和 `right` 指针的位置。根据分析结果我们知道。
元素不存在数组内时：
```markdown
left  指向第一个大于目标值的位置
right 指向第一个小于目标值的位置
```
根据这个特性，我们可以确保在目标值不在数组中时直接返回 `right+1` 能够覆盖 case 2 的所有情况，代码如下
```go
    func searchInsert(nums []int, target int) int {
        left := 0
        right := len(nums) - 1
        for left <= right {
            mid := left + (right-left)/2
            if nums[mid] == target {
                return mid
            } else if nums[mid] < target {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
        return right + 1
    }
```
**复杂度分析**
- 时间复杂度：O(log n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。




## 参考
* [代码随想录](https://programmercarl.com/0035.%E6%90%9C%E7%B4%A2%E6%8F%92%E5%85%A5%E4%BD%8D%E7%BD%AE.html)
* [leetcode 题解](https://leetcode-cn.com/problems/binary-search/solution/er-fen-cha-zhao-by-leetcode-solution-f0xw/)






