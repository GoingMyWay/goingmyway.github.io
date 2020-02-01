---
title: LeetCode 7. Reverse Integer
date: 2018-01-04 11:14:49
tags: LeetCode
category: LeetCode
---


## Question

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

***Input:*** 123
***Output:***  321

**Example** 2:

***Input:*** -123
***Output:*** -321

**Example** 3:

***Input:*** 120
***Output:*** 21

**Note: **

Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.


## Solution

If the input is smaller than zero, make it positive.


## Code


```python
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        ans = 0
        is_neg = x < 0 
        if is_neg:
            x = -x
        while x:
            ans = ans * 10 + x % 10
            x //= 10
            if ans > 2**31-1 or ans < -2**31:
                return 0
            
        return -ans if is_neg else ans 
```
