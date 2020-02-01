---
title: LeetCode 22. Generate Parentheses
date: 2018-01-14 11:25:37
tags: LeetCode
category: LeetCode
---

## Question

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]


## Solution

On LeetCode, the problem is tagged with backtracking tag, however, I think it is more a binary tree problem than a backtracking problem. My idea is we can consider thie problem as a creating a binary tree problem, where at each node '(' or ')' can be added to the tree. For example when n=3, as the following picture illustrates


![tree](tree.png)


So, at what condition can we add '(' or ')'? 

1. If the remaining numnber of  '(' is greater than 0, add '('.
2. If the number of '(' added is larger than that of ')', add ')'.
3. Recursively build a tree.


If you want to calculate the number of outputs, use [Catalan Number](https://en.wikipedia.org/wiki/Catalan_number) formula.

## Code


CPP code

```cpp
using namespace std;

class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> result;
        addingPar(result, "", n, n, n);
        return result;
    }
    void addingPar(vector<string> &v, string str, int n, int left, int right){
        if ( left==0 && right==0 ) {
            v.push_back(str);
            return;
        }
        
        if ( left > 0 ) { addingPar(v, str+"(", n, left-1, right); }
        if ( n-left > n-right ) { addingPar(v, str+")", n, left, right-1); }
    }
};
```

Python code

```python
class Solution(object):
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        result = []
        self.add_paran(result, '', n, left=n, right=n)
        return result

    def add_paran(self, result, s_str, n,  left, right):
        if left == 0 and right == 0:
            result.append(s_str)
            return

        if left > 0:
            self.add_paran(result, s_str + '(', n, left - 1, right)
        if n-left > n-right:
            self.add_paran(result, s_str + ')', n, left, right - 1)
```
