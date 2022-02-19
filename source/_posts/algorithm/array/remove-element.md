---
title: 移除元素
date: 2022-02-19
tags: ["数组"]
categories: ["算法"]
author: a东
---

## 移除元素
给你一个数组 nums和一个值 val，你需要 原地 移除所有数值等于val的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

[ leetcode 题目链接](https://leetcode-cn.com/problems/remove-element/)

示例1
```
输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2]
解释：函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。你不需要考虑数组中超出新长度后面的元素。例如，函数返回的新长度为 2 ，而 nums = [2,2,3,3] 或 nums = [2,2,0,0]，也会被视作正确答案。  
```

示例2
```
输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3]
解释：函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。注意这五个元素可为任意顺序。你不需要考虑数组中超出新长度后面的元素。
```
<!-- more -->


### 解题思路
#### 暴力求解法
首先考虑暴力求解法，因为数组在存储空间是连续的，因此移除数组中的一个元素只能通过将该元素后面的数据依次向左移一位，移除一个元素的时间复杂度为 `O(n)` 。

```cgo
    func removeElement(nums []int, val int) int {
        size := len(nums)
        for i := 0; i < size; i++ {
            if nums[i] == val {
                for j := i; j < size-1; j++ {
                    nums[j] = nums[j+1]
                }
                size = size - 1
                i = i - 1  // 可能移动过来的值仍然等于 val，需要再次处理
            }
        }
        return size
    }
```
暴力求解法的思路比较清晰，需要注意边界条件以及移除一个元素后移动过来的元素仍然等于 `val` 的情况，此时记得将 `i-1` 再次判断处理即可。

### 复杂度分析
- 时间复杂度：O(n^2)，其中 n 是数组的长度。
- 空间复杂度：O(1)。

#### 双指针法
双指针是处理数组问题中一种比较常见的算法，它的好处是能够帮助我们把一个 O(n^2) 的算法优化到 O(n)。我们指定 `slow` 和 `fast` 2个指针，`fast` 遍历数组，每次找到不等于 `val` 的元素则赋值到 `left` 指针并将 `left` 指针向前推进。
这样遍历完一遍后 `[0, left]` 就是移除 `val` 后剩余的数组了，我们直接返回它的长度即可。

```cgo
    func removeElement2(nums []int, val int) int {
        slow := 0
        fast := 0
        for ; fast < len(nums); fast++ {
            if nums[fast] != val {
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
* [代码随想录](https://www.programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html#_27-%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0)
* [leetcode 题解](https://leetcode-cn.com/problems/remove-element/solution/yi-chu-yuan-su-by-leetcode-solution-svxi/)






