---
title: 两个数组的交集
date: 2022-03-05
tags: ["哈希表"]
categories: ["算法"]
author: a东
---

## 两个数组的交集
给定两个数组 nums1 和 nums2 ，返回 它们的交集 。输出结果中的每个元素一定是 唯一 的。我们可以 不考虑输出结果的顺序 。
[ leetcode 题目链接](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

示例1
```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
```

示例2
```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
解释：[4,9] 也是可通过的
```
<!-- more -->

### 解题思路
借助 `hashmap` 记录每个数组中的不同元素，然后进行比对，每次找到相同元素将 `hashmap` 中的对应元素的存在关系置为 `false` 避免将重复元素加入结果集。


```cgo
    func intersection(nums1 []int, nums2 []int) []int {
        var res []int
        numsMap := make(map[int]bool)
        for _, num := range nums1 {
            numsMap[num] = true
        }
    
        for _, num := range nums2 {
            if numsMap[num] {
                res = append(res, num)
                numsMap[num] = false  // 避免将重复元素加入结果集
            }
        }
    
        return res
    }
```


### 复杂度分析
- 时间复杂度：O(m+n)，其中 m+n 是2个数组的长度。
- 空间复杂度：O(m+n)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/intersection-of-two-arrays/solution/liang-ge-shu-zu-de-jiao-ji-by-leetcode-solution/)






