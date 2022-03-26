---
title: 滑动窗口最大值
date: 2022-03-25
tags: ["栈&队列"]
categories: ["算法"]
author: a东
---

##  滑动窗口最大值
给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回 滑动窗口中的最大值 。

[leetcode 题目链接](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/)

示例1
```
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

示例2
```
输入：nums = [1], k = 1
输出：[1]
```
<!-- more -->


### 解题思路
使用单调递减双端队列来处理，单调递减双端队列有如下特性：

```markdown
队列中的元素从队首到队尾是单调递减的
元素可以从队首或队尾出/入队
```

处理的过程就是遍历数组并将数组元素入单调递减双端队列，要保持单调递减双端队列的特性则入队操作如下：
```markdown
若队列为空则直接入队
若队列不为空则和队尾元素比较，若当前元素大于队尾元素则队尾元素出队，重复该步骤直到当前元素小于等于队尾元素或队列为空 
```
要保留等于是因为如果等于也出队则只保证了窗口右侧而不能保证窗口左侧，在窗口向右滑动过程中会丢失最大值，如数组 `[-7,-8,7,5,7,1,6,0]` 窗口大小为 4 
当窗口左侧滑动到 -8 时若等于也出队则 当滑动窗口左侧滑动到 5 时则丢失了 最大值 7

这样入队操作可以保证当遍历到第 k 个元素时，单调递减双端队列的队首元素是 `a[0]...a[k]` 中的最大元素，肯定也是 `a[k-2], a[k-1], a[k]` 中的最大元素（假设滑动窗口大小为3）。<br>
由于滑动窗口大小限制，因此每次遍历数组元素向后推进后需要把推进前滑动窗口的队首元素出队，出队需要判断对手元素是否是要出队的元素：
```markdown
若队首元素等于元素 `a[k-3]` 则队首元素出队
否则不出队（这种情况是 a[k-3] 后面更大的元素入队把 a[k-3] 从队尾出队了，或者还在队列中）
```


```cgo
    type Deque struct {
        queue []int
    }
    
    func NewDQueue() *Deque {
        return &Deque{
            queue: make([]int, 0),
        }
    }
    
    func (q *Deque) Front() int {
        return q.queue[0]
    }
    
    func (q *Deque) Back() int {
        return q.queue[len(q.queue)-1]
    }
    
    func (q *Deque) Empty() bool {
        return len(q.queue) == 0
    }
    
    func (q *Deque) Enqueue(val int) {
        for !q.Empty() && val > q.Back() {
            q.queue = q.queue[:len(q.queue)-1]
        }
        q.queue = append(q.queue, val)
    }
    
    func (q *Deque) Dequeue() {
        if !q.Empty() {
            q.queue = q.queue[1:]
        }
    }
    
    func maxSlidingWindow(nums []int, k int) []int {
        res := make([]int, 0)
        deque := NewDQueue()
    
        for i := 0; i < k; i++ {
            deque.Enqueue(nums[i])
        }
        res = append(res, deque.Front())
    
        for i := k; i < len(nums); i++ {
            if nums[i-k] == deque.Front() {
                deque.Dequeue()
            }
    
            deque.Enqueue(nums[i])
            res = append(res, deque.Front())
        }
        return res
    }
```


### 复杂度分析
- 时间复杂度：O(n)，n 是数组长度。
- 空间复杂度：O(k)，因为不断有元素从队列弹出因此 k < n。



## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/sliding-window-maximum/solution/hua-dong-chuang-kou-zui-da-zhi-by-leetco-ki6m/)






