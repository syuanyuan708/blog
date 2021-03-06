---
title: x 的平方根
date: 2022-02-17
tags: ["数组", "二分法"]
categories: ["算法"]
author: a东
mathjax: true
---

## x 的平方根
给定一个非负整数 `x` ，计算并返回 `x` 的平方根，即实现 `int sqrt(int x)` 函数。

正数的平方根有两个，只输出其中的正数平方根。

如果平方根不是整数，输出只保留整数的部分，小数部分将被舍去。

[ leetcode 题目链接](https://leetcode-cn.com/problems/jJ0w9p/)

示例1
```
输入: x = 4
输出: 2
```

示例2
```
输入: x = 8
输出: 2
解释: 8 的平方根是 2.82842...，由于小数部分将被舍去，所以返回 2
```
<!-- more -->

### 解题思路
根据题目要求最终要求的平方根可以截断为一个整数，因此可以把问题转化为在一个 `[1,n]` 的升序数组中查找一个满足条件的平方根值。根据数组的特性 **有序**、**无重复元素**，可以直接采用二分查找算法求解。
因为 `n` 的平方根不会超过 `n/2 + 1` 因此右边界可以直接设为 `n/2 + 1`。`n` 的值存在如下2种情况：
```markdown
n 是一个完全平方数，那么能恰好查找到对应的平方根值。
n 不是一个完全平方数，那么返回小于浮点型平方根的第一个整数。
```
针对第2种情况，同样可以使用我们在二分查找算法文章 [二分查找算法-运行结果分析](/2022/02/15/binary-search/) 一节中分析所得的结论，即目标值不在数组中时，查找结束后 `right` 指向小于目标值的第一个元素。
**因此对于 `n` 为非完全平方数的情况我们可以直接返回 `right`**

```cgo
    func mySqrt(n int) int {
        left := 0
        right := n/2 + 1
        for left <= right {
            mid := left + (right-left)/2
            if mid*mid == n {
                return mid
            } else if mid*mid < n {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
        return right
    }
```

### 复杂度分析
- 时间复杂度：O(log n)，其中 n 是数组的长度。
- 空间复杂度：O(1)。


## x 的平方根 V2
还是求一个数的平方根，但是要求精确到小数点后2位，进位不采取四舍五入的方式。

### 思路
计算平方根已经有一些成熟的数学算法，其中牛顿迭代法是比较常见的一种，下面来简单介绍一下
![牛顿法](/images/algorithm/array/niu-dun.png)
使用牛顿法用来迭代的求解一个方程：
对于一个函数 `f(x)`,它的泰勒级数展开式是这样的
$$𝑓(𝑥)=𝑓(𝑥_0)+𝑓'(𝑥_0)(𝑥−𝑥_0)+\frac{1}{2}𝑓''(𝑥_0)(𝑥−𝑥_0)^2+...+\frac{1}{n!}𝑓^𝑛(𝑥_0)(𝑥−𝑥_0)^𝑛$$

当使用牛顿法来求一个方程解的时候，它使用泰勒级数前两项来代替这个函数，因此可以简化为:
$$𝑓(𝑥)=𝑓(𝑥_0)+𝑓'(𝑥_0)(𝑥−𝑥_0)$$
令𝑓(𝑥)=0，则 $$x = x_0 - \frac{𝑓(𝑥_0)}{𝑓'(𝑥_0)}$$
所以，牛顿法的迭代公式是 $$x_𝑛+1=x_𝑛−\frac{𝑓(x_𝑛)}{𝑓'(x_𝑛)}$$

牛顿法求解n的平方根
求解n的平方根，其实是求方程 $$x^2−n = 0$$ 的解
利用上面的公式可以得到：$$x_𝑖+1=x_𝑖−\frac{x_𝑖^2−n}{2x_𝑖} = (x_𝑖+\frac{n}{x_𝑖})/2$$
编程的时候核心的代码是：$$x = (x + \frac{n}{x})/2$$

代码如下
```cgo
    func mySqrt(n float64) float64 {
        q := n
        for math.Abs(q*q-n) > 0.00000001 {
            q = (q + n/q) / 2
        }
    
        value, _ := strconv.ParseFloat(fmt.Sprintf("%.2f", q), 64)
        return value
    }
```


## 参考
* [牛顿迭代法](https://zh.wikipedia.org/wiki/%E7%89%9B%E9%A1%BF%E6%B3%95)





