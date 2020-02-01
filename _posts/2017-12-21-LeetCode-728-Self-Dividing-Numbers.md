---
title: LeetCode 728. Self Dividing Numbers
date: 2017-12-21 15:41:47
tags: LeetCode
category: LeetCode
---

The question is pretty easy

## Question

A self-dividing number is a number that is divisible by every digit it contains.

For example, 128 is a self-dividing number because 128 % 1 == 0, 128 % 2 == 0, and 128 % 8 == 0.

Also, a self-dividing number is not allowed to contain the digit zero.

Given a lower and upper number bound, output a list of every possible self dividing number, including the bounds if possible.

** Example 1: **

```
Input: 
left = 1, right = 22
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]
```

** Note: **

* The boundaries of each input argument are 1 <= left <= right <= 10000.


## Solution

Loop each value in the range and check if current value is a self-dividing number


## Code


```python
class Solution(object):
    def selfDividingNumbers(self, left, right):
        """
        :type left: int
        :type right: int
        :rtype: List[int]
        """
        outputs = []
        for number in range(left, right+1):
            for v in str(number):
                if int(v) == 0 or number % int(v) != 0:
                    break
            else:
                outputs.append(number)
        return outputs
```

