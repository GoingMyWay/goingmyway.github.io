---
title: LeetCode 412. Fizz Buzz
date: 2018-01-03 21:22:59
tags: LeetCode
category: LeetCode
---

## Question


Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output "Fizz" instead of the number and for the multiples of five output "Buzz". For numbers which are multiples of both three and five output "FizzBuzz".

Example:

n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]


## Solution

The solution is simple


## Code


```python
class Solution(object):
    def fizzBuzz(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        outputs = []
        for i in range(1, n+1):
            if i % 3 == 0 and i % 5 != 0:
                outputs.append('Fizz')
            elif i % 3 !=0  and i % 5 == 0:
                outputs.append('Buzz')
            elif i % 3 == 0 and i % 5 == 0:
                outputs.append('FizzBuzz')
            else:
                outputs.append(str(i))
        return outputs

```

Or more clean one

```python
class Solution(object):
    def fizzBuzz(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        return ['Fizz' * (not i % 3) + 'Buzz' * (not i % 5) or str(i) for i in range(1, n+1)]
```
