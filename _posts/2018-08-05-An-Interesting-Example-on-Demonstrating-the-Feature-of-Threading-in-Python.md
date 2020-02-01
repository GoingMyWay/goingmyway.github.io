---
title: 'An Interesting Example on Demonstrating the Feature of Threading in Python '
date: 2018-08-05 16:42:43
tags: Python
categories: Python
---

Threading in Python is fake parallelism due to GIL, and in TensorFlow, the TF code will release the GIL when runing the C++ code in parallel. The best practise of using multi-thread in Python is to do tasks with high I/O and low CPU intensity. For high I/O, here is an example.


```Python
In [1]: import requests, threading

In [2]: from time import time

In [3]: def downloader():
   ...:     starttime = time()
   ...:     requests.get('http://ipv4.download.thinkbroadband.com/100MB.zip')
   ...:     print('download finished in {:.2f} seconds'.format((time()-starttime)))
   ...: 

In [4]: def tasklauncher():
   ...:     starttime = time()
   ...:     threads = [threading.Thread(target=downloader) for i in range(2)]
   ...:     for t in threads:
   ...:         t.start()
   ...:     for t in threads:
   ...:         t.join()
   ...:     print('tasklauncher finished in {:.3f} seconds'.format((time()-starttime)))
   ...: 

In [5]: tasklauncher()
download finished in 50.90 seconds
download finished in 49.34 seconds
tasklauncher finished in 50.89 seconds

In [6]: downloader()
download finished in 48.09 seconds
```

As you can see the result, by using multi-thread, it is 2 times faster than using a single thread. How about using multi-threading to do CPU intensive computing task? Here we go.


```Python
In [1]: from time import time

In [2]: import threading

In [3]: def compute_task():
   ...:     starttime = time()
   ...:     sum_v = 0
   ...:     for i in range(100000000):
   ...:         sum_v += i
   ...:     print('finished in {:.3f} seconds'.format((time()-starttime)))
   ...:     

In [4]: def compute_task_launcher():
   ...:     starttime = time()
   ...:     threads = [threading.Thread(target=compute_task) for _ in range(2)]
   ...:     for t in threads:
   ...:         t.start()
   ...:     for t in threads:
   ...:         t.join()
   ...:     print('compute_task_launcher finished in {:.3f} seconds'.format((time()-starttime)))
   ...:     

In [5]: compute_task_launcher()
finished in 14.670 seconds
finished in 14.667 seconds
compute_task_launcher finished in 14.689 seconds

In [6]: def compute_task_launcher2():
   ...:     starttime = time()
   ...:     threads = [threading.Thread(target=compute_task) for _ in range(2)]
   ...:     for t in threads:
   ...:         t.start()
   ...:         t.join()
   ...:     print('compute_task_launcher finished in {:.3f} seconds'.format((time()-starttime)))
   ...:     

In [7]: compute_task_launcher2()
finished in 7.077 seconds
finished in 7.100 seconds
compute_task_launcher finished in 14.177 seconds
```

As you can see the result, by launching 2 threads, the total time is 14.689 seconds, and each thread costs 14.670, looks they ran in parallel, didnot they? However, by checking the result of function `compute_task_launcher2()` you will see that in fact when running serially, the computation task only cost 7.077 seconds, approximatly half of that in multi-threadings.

And the total time cost in serialized threading is 14.177, slightly smaller than that of multi-theading. In conclusion, nearly 3% loss of time based on your computer and OS regardless of how many threads you spwan.

