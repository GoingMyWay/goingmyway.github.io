---
title: LeetCode 357. Count Numbers with Unique Digits
date: 2017-11-03 16:43:08
tags: LeetCode
categories: LeetCode
---

## Question

Given a non-negative integer n, count all numbers with unique digits, x, where 0 <= x < 10^n.

Example:
Given n = 2, return 91. (The answer should be the total numbers in the range of 0 <= x < 100, excluding [11,22,33,44,55,66,77,88,99])

Credits:
Special thanks to @memoryless for adding this problem and creating all test cases.

## Solution

Here both dynamic programming and backtracking are good methods to tackle this problem, I will explain the detailed solution behind DP.

If you have learnt combination in mathmatics you will know that bascically this problem is a kind of combination problem, and here we go.


Since duplicated digits are not allowed in a number, and the leading zero is a nasty situation, we can count the number by the length of the number. For example, given n=3, and we get x between 0 and 999, so the length of a number in this range may be len=1, 2 or 3. Let us count the total number of all the numbers in this range.

Firstly, when len=1, apparently, the number is 10, that is result=10

And when len=2, since the highest digit is 0, and the the result=9*9, the first nine means there are 9 choices except for 0, and the second nine means there are 9 choices except for the number chosed in the previous digit.

And when len=2, there is no doubt that there are 9*9 result in the first 2 digits and for the last digit, since normally there are 10 choices, however 2 choices should be excluded and there are 8 choices. So the result=9*9*8.

In sum, the answer is 10+9*9+9*9*8=739.


To sum up, 

when i==2, count=9\*(10-(i-1)).
when i==3, count=9\*9\*(10-(i-1)).
...
when i==10, count=9\*9\*8..\*(10-(i-1))

the maximum value of n is 10.



## Accepted Code

```python
class Solution(object):
    def countNumbersWithUniqueDigits(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 0:
            return 1
        dp = [0, 10] + [9]*(n-1)
        for i in xrange(2, n+1):
            if i == 2:
                dp[i] = 9 * (10-i+1)
            else:
                dp[i] = dp[i-1] * (10-i+1)
        return sum(dp)
```
