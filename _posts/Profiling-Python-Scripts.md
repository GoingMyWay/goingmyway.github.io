---
title: Profiling Python Scripts
date: 2018-08-13 16:21:20
tags: Python
categories: Python
---

Profiling Python scripts can help improving the performance and reduce time costs. This post introduces profiling and a visual tool [SNAKEVIZ](http://jiffyclub.github.io/snakeviz/) to visualize the profile output data. Python can be very slow in pure Python without C/C++ bindings. Profiling helps to detect the total time costs and output which part of the code consumes time most. 

One can easily generate the profile data by runing `cProfile` module,

```shell
python3.6 -m cProfile -o profile.dat YUO_PROGRAMME.py
```
And using SNAKEVIZ, it can render the profile data on a web page.

```shell
snakeviz profile.dat
```

Next ... 

