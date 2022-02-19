---
title: 删除有序数组中的重复项
date: 2022-02-19
tags: ["数组"]
categories: ["算法"]
author: a东
---

## 删除有序数组中的重复项
给你一个 升序排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。

由于在某些语言中不能改变数组的长度，所以必须将结果放在数组nums的第一部分。更规范地说，如果在删除重复项之后有 k 个元素，那么nums的前 k 个元素应该保存最终结果。

将最终结果插入nums 的前 k 个位置后返回 k 。

不要使用额外的空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

[ leetcode 题目链接](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

示例1
```
输入：nums = [1,1,2]
输出：2, nums = [1,2,_]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。 
```

示例2
```
输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
```
<!-- more -->


### 解题思路
#### 双指针法
采用双指针解法，首先保留位置为0的元素，`slow` 和 `fast` 初始时都指向位置为1的元素，`fast` 依次向后遍历数组每次当前元素和它的前一个元素不相等时将当前元素赋值给 `slow` 并将 `slow` 向前推进。

```cgo
    func removeDuplicates(nums []int) int {
        slow := 1
        fast := 1
        for ; fast < len(nums); fast++ {
            if nums[fast] != nums[fast-1] {
                nums[slow] = nums[fast]
                slow = slow + 1
            }
        }
    
        return slow
    }
```
### 复杂度分析
- 时间复杂度：O(log n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。




## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/solution/shan-chu-pai-xu-shu-zu-zhong-de-zhong-fu-tudo/)






