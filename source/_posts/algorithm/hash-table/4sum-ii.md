---
title:  四数相加 II
date: 2022-03-05
tags: ["哈希表"]
categories: ["算法"]
author: a东
---

##  四数相加 II
给你四个整数数组 nums1、nums2、nums3 和 nums4 ，数组长度都是 n ，请你计算有多少个元组 (i, j, k, l) 能满足：

0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0
[ leetcode 题目链接](https://leetcode-cn.com/problems/4sum-ii/)

示例1
```
输入：nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
输出：2
解释：
两个元组如下：
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
```
<!-- more -->

示例2
```
输入：nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
输出：1
```

### 解题思路
题目要求计算四个数组 `nums1`、`nums2`、`nums3`、`nums4` 中各取一个元素相加和为0的组合个数，问题可以转换为： `nums1`、`nums2` 中各取一个元素的和记为 `A`，`nums3`、`nums4`
中各取一个元素的和记为 `B` 满足 `A+B = 0` 的组合的个数。因此可以按照如下步骤进行求解：

```markdown
先用 hashtable 统计 nums1、nums2 中各取一个元素的和及其出现的次数
用上面遍历得到的 hashtable 遍历 nums3、nums4 各取一个元素的和记为 B，求 hashtable 中值为 -B 的元素的个数，将满足条件的个数相加得到最后结果。
```

```cgo
    func fourSumCount(nums1 []int, nums2 []int, nums3 []int, nums4 []int) int {
        cnt := 0
        numsMap := make(map[int]int)
        for _, num1 := range nums1 {
            for _, num2 := range nums2 {
                numsMap[num1+num2]++
            }
        }
    
        for _, num3 := range nums3 {
            for _, num4 := range nums4 {
                cnt += numsMap[-num3-num4]
            }
        } 
        return cnt
    }
```


### 复杂度分析
- 时间复杂度：O(n^2)，其中 n 是数组长度。
- 空间复杂度：O(n^2)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/4sum-ii/solution/si-shu-xiang-jia-ii-by-leetcode-solution/)






