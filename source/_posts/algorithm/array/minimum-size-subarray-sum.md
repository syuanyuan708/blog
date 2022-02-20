---
title: 长度最小的子数组
date: 2022-02-20
tags: ["数组", "滑动窗口"]
categories: ["算法"]
author: a东
---

## 长度最小的子数组
给定一个含有 n 个正整数的数组和一个正整数 target 。

找出该数组中满足其和 ≥ target 的长度最小的 连续子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

[ leetcode 题目链接](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

示例1
```
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
```

示例2
```
输入：target = 4, nums = [1,4,4]
输出：1
```
<!-- more -->

示例3
```
输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
```

### 解题思路
采用滑动窗口来进行处理，滑动窗口其实是双指针的一种用法。首先明确下窗口的移动
```markdown
如果当前和小于目标值，则窗口不断向右扩展
一但当前和大于等于目标值，则窗口开始逐渐收缩直到找到满足条件的最小窗口
```

以 `示例1` 为例，窗口从数组位置0开始向右扩展当扩展到 `[2,3,1,2]` 时窗口内元素和大于等于目标值，此时尝试收缩窗口来寻找更小长度的窗口，因此只要窗口内元素的和大于等于目标值则不断将窗口的左侧向右推进。
推进1次后 `[3,2,1]` 不满足大于等于目标值了，此时只能继续向右扩展窗口进行查找，重复执行上述过程直到遍历遍历完整个数组。

```cgo
    func minSubArrayLen(target int, nums []int) int {
        left := 0  // 窗口左侧
        right := 0 // 窗口右侧
        minLen := math.MaxInt32
        sum := 0
        for ; right < len(nums); right++ {
            sum = sum + nums[right] // 扩展窗口
            for sum >= target {
                if right - left + 1 < minLen {
                    minLen = right - left + 1
                }
                sum = sum - nums[left] // 收缩窗口
                left = left + 1
            }
        }
    
        if minLen == math.MaxInt32 {
            return 0
        }
        return minLen
    }
```

### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。




## 参考
* [代码随想录](https://www.programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html#_209-%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84)
* [leetcode 题解](https://leetcode-cn.com/problems/minimum-size-subarray-sum/solution/chang-du-zui-xiao-de-zi-shu-zu-by-leetcode-solutio/)






