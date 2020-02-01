---
title: Getting the Product of a Python List
date: 2018-08-11 23:04:06
tags: Python
categories: Python
---

Given a list, get the product of the list, for example a list `[1, 2, 3]` and its product is `1*2*3=6`.

```python
>>> a = [1, 2, 3]
>>> get_product(a)
6
```

### Method 1

Using `numpy`'s `prod`


### Method 2

Using `functools.reduce` and `operator.mul`


```python
>>> a = [1, 2, 3]
>>> import functools
>>> import operator
>>> b = functools.reduce(operator.mul, a, 1)
>>> b
6
```


### Reference

* https://stackoverflow.com/questions/2104782/returning-the-product-of-a-list
* https://www.geeksforgeeks.org/python-multiply-numbers-list-3-different-ways/

