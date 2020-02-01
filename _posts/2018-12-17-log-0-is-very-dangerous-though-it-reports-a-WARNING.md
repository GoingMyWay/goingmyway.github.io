---
title: log(0) is very dangerous though it reports a WARNING
date: 2018-12-17 15:38:31
tags: Python
category: Python
---

In mathematics, $log(0)$ is undefined, its value is not a real number. And in numpy it will return `-inf`. However, in RL code it will report WARNING on the zero value that may lead NaN error later in your code, which can be very hard to debug. So here I recommend adding a additional value for example `0.00000001` or checking the input value to avoid potential NaN errors.

```Python
In [23]: np.log(0)
/Library/Frameworks/Python.framework/Versions/3.6/bin/ipython3:1: RuntimeWarning: divide by zero encountered in log
Out[23]: -inf
```

