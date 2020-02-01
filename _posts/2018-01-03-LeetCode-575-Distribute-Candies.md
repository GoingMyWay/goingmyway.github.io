---
title: LeetCode 575. Distribute Candies
date: 2018-01-03 21:05:14
tags: LeetCode
category: LeetCode
---


## Question

Given an integer array with even length, where different numbers in this array represent different kinds of candies. Each number means one candy of the corresponding kind. You need to distribute these candies equally in number to brother and sister. Return the maximum number of kinds of candies the sister could gain.

** Example 1: **
*** Input: *** candies = [1,1,2,2,3,3]
*** Output: 3 ***
*** Explanation: ***
There are three different kinds of candies (1, 2 and 3), and two candies for each kind.
Optimal distribution: The sister has candies [1,2,3] and the brother has candies [1,2,3], too. 
The sister has three different kinds of candies. 

** Example 2: **

*** Input:*** candies = [1,1,2,3]
*** Output:*** 2
*** Explanation:*** For example, the sister has candies [2,3] and the brother has candies [1,1]. 
The sister has two different kinds of candies, the brother has only one kind of candies. 

** Note: **

The length of the given array is in range [2, 10,000], and will be even.
the number in given array is in range [-100,000, 100,000].## Code


## Solution

the solution is from [LeetCode](https://discuss.leetcode.com/topic/88510/python-straightforward-with-explanation), I think its very simple and elegant, so I share its here.

My solution is, first I can get the count of each kind of candies and for each kind of candies, pick only one candy, if the value of picked candies equals len(candies)//2, return the number of kinds of candies. Else, return the number of kinds of candies of the original candy list


## Code


Code from LeetCode


```python
class Solution:
    def distributeCandies(self, candies):
        """
        :type candies: List[int]
        :rtype: int
        """
        return min(len(candies)//2, len(set(candies)))
```

My solution

```python
class Solution(object):
    def distributeCandies(self, candies):
        """
        :type candies: List[int]
        :rtype: int
        """
        import collections
        counter = collections.Counter(candies)
        all_sum = 0
        count = 0
        for k, v in counter.iteritems():
            all_sum += 1
            count += 1
            if all_sum == len(candies) / 2:
                return count
    
        return len(counter)
```

Basically, the ideas behind the above code are similar, but the time complexity of my solution is larger than that of code from LeetCode, since its straightforward and simple.
