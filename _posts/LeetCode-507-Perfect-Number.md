---
title: LeetCode 507. Perfect Number
date: 2017-12-21 17:02:06
tags: LeetCode
category: LeetCode
---

## Question


We define the Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself.

Now, given an integer n, write a function that returns true when it is a perfect number and false when it is not.
** Example: **
```
Input: 28
Output: True
Explanation: 28 = 1 + 2 + 4 + 7 + 14
```

** Note: ** The input number n will not exceed 100,000,000. (1e8)


## Solution

You will get TLE(Time Limit Exceeded) if you simply loop all the values. So, to tackle this problem, there is a theorem that is: if number n is not a prime, there must be a factor d among the range of 2 and sqrt(n), the factor d is very important for none-prime numbers.

## Code

```python
class Solution(object):
    def checkPerfectNumber(self, num):
        """
        :type num: int
        :rtype: bool
        """
        if num <= 0: return False
        ans, sqrt = 0, int(num**0.5)
        ans = sum(v+num//v for v in xrange(1, sqrt+1) if num%v==0)
        if sqrt ** 2 == num:
            ans -= sqrt
        return ans-num==num
```

Just check every i from 1 to sqrt(num). When num % i == 0, we add both i and num//i to our result. And remember to exclude the num itself and check if we added a duplicate sqrt(num) in the end. 

