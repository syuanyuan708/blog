---
title:  两数之和
date: 2022-03-05
tags: ["哈希表"]
categories: ["算法"]
author: a东
---

##  两数之和
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。
[ leetcode 题目链接](https://leetcode-cn.com/problems/two-sum/)

示例1
```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

示例2
```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```
<!-- more -->

### 解题思路
用 `hashtable` 记录数组每个元素的位置，遍历一遍即可计算出结果。


```cgo
    func twoSum(nums []int, target int) []int {
        numsMap := make(map[int]int)
        for i, num := range nums {
            if _, ok := numsMap[target-num]; ok {
                return []int {i, numsMap[target-num]}
            }
            numsMap[num] = i
        }
        return []int {-1, -1}
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组长度。
- 空间复杂度：O(n)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/two-sum/solution/liang-shu-zhi-he-by-leetcode-solution/)






