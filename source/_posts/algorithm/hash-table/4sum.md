---
title:  四数之和
date: 2022-03-06
tags: ["哈希表"]
categories: ["算法"]
author: a东
---

##   四数之和
给你一个由 n 个整数组成的数组 nums ，和一个目标值 target 。请你找出并返回满足下述全部条件且不重复的四元组 [nums[a], nums[b], nums[c], nums[d]] （若两个四元组元素一一对应，则认为两个四元组重复）：

0 <= a, b, c, d < n
a、b、c 和 d 互不相同
nums[a] + nums[b] + nums[c] + nums[d] == target
你可以按 任意顺序 返回答案 。
[ leetcode 题目链接](https://leetcode-cn.com/problems/4sum/)

示例1
```
输入：nums = [1,0,-1,0,-2,2], target = 0
输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

示例2
```
输入：nums = [2,2,2,2,2], target = 8
输出：[[2,2,2,2]]
```
<!-- more -->


### 解题思路
解题思路和 `三数之和` 基本一致，需要注意一点，不能在 `nums[i] > target` 时结束查找，因为 target 可能是一个负数，整数相加是单调递增的，负数相加是单调递减的，可以下如下例子：
- 数组 `[1,-2,-5,-4,-3,3,3,5]` , `target = -11` ，数组排序后 `[-5, -4, -3, -2, 1, 3, 3, 5]` 第一个元素 `-5` 已经大于 target 了，但是它存在一个满足条件的组合 `[-5,-4,-3,1]`


```cgo
    func fourSum(nums []int, target int) [][]int {
        res := make([][]int, 0)
        sort.Ints(nums)
        for i := 0; i < len(nums) - 3; i++ {
            if i > 0 && nums[i] == nums[i-1] {
                continue
            }
            for j := i + 1; j < len(nums) - 2; j++ {
                if j > i + 1 && nums[j] == nums[j-1] {
                    continue
                }
                left  := j + 1
                right := len(nums) - 1
                for left < right {
                    if nums[i]+nums[j]+nums[left]+nums[right] == target {
                        res = append(res, []int{nums[i], nums[j], nums[left], nums[right]})
                        for left + 1 < right && nums[left] == nums[left+1] {
                            left++
                        }  
                        left++
                        for left < right - 1 && nums[right] == nums[right-1] {
                            right--
                        }
                        right--
                    } else if nums[i]+nums[j]+nums[left]+nums[right] < target {
                        for left + 1 < right && nums[left] == nums[left+1] {
                            left++
                        }  
                        left++
                    } else {
                        for left < right - 1 && nums[right] == nums[right-1] {
                            right--
                        }
                        right--
                    }
                }
            }
        }
        return res
    }
```


### 复杂度分析
- 时间复杂度：O(n^3)，其中 n 是数组长度。
- 空间复杂度：O(log n)，只考虑了排序所需额外空间。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/4sum/solution/si-shu-zhi-he-by-leetcode-solution/)






