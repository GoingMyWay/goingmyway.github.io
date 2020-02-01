---
title: LeetCode 401. Binary Watch
date: 2017-11-03 19:29:21
tags: LeetCode
categories: LeetCode
---

## Question

A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59).

Each LED represents a zero or one, with the least significant bit on the right.

![binary watch](Binary_clock_samui_moon.jpg)

For example, the above binary watch reads "3:25".

Given a non-negative integer n which represents the number of LEDs that are currently on, return all possible times the watch could represent.

**Example:**

Input: n = 1
Return: ["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]

**Note:**

* The order of output does not matter.
* The hour must not contain a leading zero, for example "01:00" is not valid, it should be "1:00".
* The minute must be consist of two digits and may contain a leading zero, for example "10:2" is not valid, it should be "10:02".


## Solution

Since there are 10 LEDs. So from the upleft to the bottom right, each item has indexed from 0 to 9. We can apply backtracking to tackle this problem. And for backtracking, one must know where is the terminal state and how to back to the previous state, which is of great significance.


## Accepted Code

```python
class Solution(object):
    def readBinaryWatch(self, num):
        """
        :type num: int
        :rtype: List[str]
        """
        if num > 10 or num < 0:
            return []

        result = []

        def back_tracking(start, cnt, indices):
            if cnt == num:
                self.convert2time(result, indices)
                return
            for st in range(start+1, 10):
                back_tracking(st, cnt+1, indices+[st])
        back_tracking(-1, 0, [])
        return result

    @staticmethod
    def convert2time(result, indices):
        hour, minutes = 0, 0
        for v in indices:
            if v <= 3:
                hour += 2 ** (4-v-1)
            else:
                minutes += 2 ** (10-v-1)
        if hour <= 11 and minutes <= 59:
            result.append("%s:%s" % (hour, minutes) if minutes >= 10 else "%s:0%s" % (hour, minutes))
```
