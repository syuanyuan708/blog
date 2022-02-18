---
title: 二分查找
date: 2022-02-15
tags: ["二分法"]
categories: ["算法"]
author: a东
---

## 二分查找
给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。
[ leetcode 题目链接](https://leetcode-cn.com/problems/binary-search/)

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

### 解题思路
二分查找算法的前提条件是数组有序，且数组中无重复元素（否则无法确定唯一位置）。二分法中边界条件需要根据循环不变量来确定，即在查找的过程中始终保持边界不变量。
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

### 运行结果分析
在上面的二分查找算法中，运行结果无外乎2种情况
1. 目标值在数组中，返回目标值在数组中的位置
2. 目标值不在数组中，返回 -1

**然而**对于第2种情况我们进一步分析，又可以细分为如下3种情况：

case1: 目标值在数组范围之内，但不在数组内
```markdown
输入: nums = [-1,0,3,5,9,12], target = 2     
输出: -1
查找结束后: left = 2, right = 1
```

case2: 目标值小于数组最小值
```markdown
输入: nums = [-1,0,3,5,9,12], target = -2     
输出: -1
查找结束后: left = 0, right = -1
```

case3: 目标值大于数组最大值
```markdown
输入: nums = [-1,0,3,5,9,12], target = 30     
输出: -1
查找结束后: left = 6, right = 5
```

**综合上述3种case我们可以得出一个结论：**
- **二分查找结束后若目标值不在数组中则 `left` 指向大于目标值的第一个位置，`right` 指向小于目标值的第一个位置。**
**这个结论在处理一些二分查找算法的变形问题时会比较有用，我们会在后续的相关算法题中用到它，到时候再结合具体题目进行分析相信能够加深大家的理解。**

### 复杂度分析
- 时间复杂度：O(log n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。

## 参考
* [代码随想录](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html#_704-%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE)
* [leetcode 题解](https://leetcode-cn.com/problems/binary-search/solution/er-fen-cha-zhao-by-leetcode-solution-f0xw/)






