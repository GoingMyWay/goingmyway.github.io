---
title: LeetCode 669. Trim a Binary Search Tree
date: 2018-01-03 20:27:13
tags: LeetCode
category: LeetCode
---

## Question:

Given a binary search tree and the lowest and highest boundaries as L and R, trim the tree so that all its elements lies in [L, R] (R >= L). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

** Example 1: **
*** Input: ***

```
    1
   / \
  0   2

  L = 1
  R = 2
```

*** Output: ***

```
    1
      \
       2
```

** Example 2: **
*** Input:  *** 

```
    3
   / \
  0   4
   \
    2
   /
  1

  L = 1
  R = 3
```

*** Output: ***

```
      3
     / 
   2   
  /
 1
```


## Solution

The problem is pretty simple, follow the following steps and use recursion method

* If the val of current node is smaller than L, abandon the left sub-tree and trim its right sub-tree
* If the val of current node is greater than R, abandon the right sub-tree and trim its left sub-tree
* Else, recursively trim its left and right sub-tree and return the root


## Code

```python
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Solution(object):
    def trimBST(self, root, L, R):
        """
        :type root: TreeNode
        :type L: int
        :type R: int
        :rtype: TreeNode
        """
        if not root:
            return None
        if root.val < L:
            return self.trimBST(root.right, L, R)
        elif root.val > R:
            return self.trimBST(root.left, L, R)
        
        root.left = self.trimBST(root.left, L, R)
        root.right = self.trimBST(root.right, L, R)
        return root
```
