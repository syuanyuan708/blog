---
title: 二分查找
date: 2022-02-15
tags: ["二分法"]
categories: ["算法"]
author: a东
---

## 二分查找
给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。[ leetcode 题目链接](https://leetcode-cn.com/problems/binary-search/)

示例1
```
输入: nums = [-1,0,3,5,9,12], target = 9     
输出: 4       
解释: 9 出现在 nums 中并且下标为 4    
```

示例2
```
输入: nums = [-1,0,3,5,9,12], target = 2     
输出: -1        
解释: 2 不存在 nums 中因此返回 -1    
```
<!-- more -->

### 题解思路
二分查找算法的前提条件是数组有序，且数组中无重复元素（否则无法确定唯一位置）。二分法中边界条件需要根据循环不变量来确定，即在查找的过程中保持边界不变量。
一般写二分法区间边界分为两种 [left, right] 或 [left, right)，下面采用前者来进行处理

```go
func binarySearch(nums []int, target int) int {
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

	return -1
}
```

**复杂度分析**
- 时间复杂度：O(logn)，其中 n 是数组的长度。
- 空间复杂度：O(1)。

## 参考
* [代码随想录](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html#_704-%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE)
* [leetcode 题解](https://leetcode-cn.com/problems/binary-search/solution/er-fen-cha-zhao-by-leetcode-solution-f0xw/)






