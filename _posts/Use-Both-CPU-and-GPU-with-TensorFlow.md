---
title: Use Both CPU and GPU with TensorFlow
date: 2018-10-05 11:20:51
tags: TensorFlow
categories: TensorFlow
---
One can use the following code to use CPU TensorFlow if you install GPU TensorFlow

```python
import os
os.environ["CUDA_DEVICE_ORDER"] = "PCI_BUS_ID"
os.environ['CUDA_VISIBLE_DEVICES'] = '-1'
```

So you can install Tensorflow-GPU only and switch CPU and GPU.


Reference:

* https://github.com/keras-team/keras/issues/6997#issuecomment-348332803
