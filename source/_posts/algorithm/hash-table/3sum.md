---
title:  三数之和
date: 2022-03-06
tags: ["哈希表"]
categories: ["算法"]
author: a东
---

##  三数之和
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。

注意：答案中不可以包含重复的三元组。
[ leetcode 题目链接](https://leetcode-cn.com/problems/3sum/)

示例1
```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

示例2
```
输入：nums = []
输出：[]
```
<!-- more -->

示例3
```
输入：nums = [0]
输出：[]
```

### 解题思路
题目要求结果集中不能出现重复的三元组，若使用 `hashtable` 去重处理会比较麻烦，可以采用双指针来解决。处理步骤如下
```markdown
首先对原数组 `nums` 进行排序
对排序的数组进行遍历处理， `i` 指向每轮遍历起始位置，`left` 指向 `i` 的下一个位置，`right` 指向数组末尾。每次计算 `nums[i]+nums[left]+nums[right]` 的值
    若值为 0 则加入结果集并向右扫描 `left` 去除重复元素，向左扫描 `right` 去除重复元素，别忘了最后左右指针要多移动一下跳到非重复元素
    若值大于 0 因为原数组排好序，则 `right` 左移，并跳过重复元素
    若值小于 0 则 `left` 右移，并跳过重复元素
最后如果 `nums[i] == nums[i-1]` ，即当前元素与前一个元素相等也应该跳过避免结果重复
```


```cgo
    func threeSum(nums []int) [][]int {
        res := make([][]int, 0)
        sort.Ints(nums)
        for i := 0; i < len(nums) - 2; i++ {
            if nums[i] > 0 {
                break // 后面不会再有满足条件的组合
            }
            if i > 0 && nums[i] == nums[i-1] {
                continue
            }
            left  := i + 1
            right := len(nums) - 1
            for left < right {
                if nums[i] + nums[left] + nums[right] == 0 {
                    res = append(res, []int{nums[i], nums[left], nums[right]})
                    for left + 1 < right && nums[left] == nums[left+1] {
                        left++
                    }
                    left++
                    for left < right - 1 && nums[right] == nums[right] - 1 {
                        right--
                    } 
                    right--
                } else if nums[i] + nums[left] + nums[right] < 0 {
                    for left + 1 < right && nums[left] == nums[left+1] {
                        left++
                    }
                    left++
                } else {
                    for left < right - 1 && nums[right] == nums[right] - 1 {
                        right--
                    } 
                    right--
                }
            }
        }
        return res
    }
```


### 复杂度分析
- 时间复杂度：O(n^2)，其中 n 是数组长度。
- 空间复杂度：O(log n)，只考虑了排序所需额外空间。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/3sum/solution/san-shu-zhi-he-by-leetcode-solution/)






