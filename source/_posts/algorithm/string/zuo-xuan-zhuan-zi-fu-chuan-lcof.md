---
title:  左旋转字符串
date: 2022-03-13
tags: ["字符串"]
categories: ["算法"]
author: a东
---

##  左旋转字符串
字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

[leetcode 题目链接](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

示例1
```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

示例2
```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

<!-- more -->

### 解题思路
先拷贝后半部分再拷贝前半部分，计算好下标之间的关系就好。


```cgo
    func reverseLeftWords(s string, n int) string {
        sbytes := make([]byte, len(s))
        for i := n; i < len(s); i++ {
            sbytes[i-n] = s[i]
        }
    
        for i := 0; i < n; i++ {
            sbytes[len(s) - n + i] = s[i]
        }
        return string(sbytes)
    }
```


### 复杂度分析
- 时间复杂度：O(n)，其中 n 是字符串长度。
- 空间复杂度：O(n)。

## 参考
* [leetcode 题解](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/solution/mian-shi-ti-58-ii-zuo-xuan-zhuan-zi-fu-chuan-qie-p/)






