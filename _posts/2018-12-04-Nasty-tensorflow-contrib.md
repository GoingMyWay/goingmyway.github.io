---
title: Nasty tensorflow.contrib
date: 2018-12-04 20:51:00
tags: TensorFlow
category: TensorFlow
---


Tensorflow is a great library for Machine Intelligence, and many people contribute this library by `tensorflow.contrib` which fosters its popularity and application. However today, I found this sub-package can be very nasty because its dependencies that can be in a mass and out of control, for example  importing `tf.contrib.layers.full_connected` can report the following error:

```python
Traceback (most recent call last):
  File "train.py", line 9, in <module>
    import tensorflow.contrib.layers as layers
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/__init__.py", line 39, in <module>
    from tensorflow.contrib import distributions
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/distributions/__init__.py", line 40, in <module>
    from tensorflow.contrib.distributions.python.ops.estimator import *
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/distributions/python/ops/estimator.py", line 21, in <module>
    from tensorflow.contrib.learn.python.learn.estimators.head import _compute_weighted_loss
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/learn/__init__.py", line 95, in <module>
    from tensorflow.contrib.learn.python.learn import *
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/learn/python/__init__.py", line 28, in <module>
    from tensorflow.contrib.learn.python.learn import *
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/learn/python/learn/__init__.py", line 30, in <module>
    from tensorflow.contrib.learn.python.learn import estimators
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/learn/python/learn/estimators/__init__.py", line 302, in <module>
    from tensorflow.contrib.learn.python.learn.estimators.dnn import DNNClassifier
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/learn/python/learn/estimators/dnn.py", line 35, in <module>
    from tensorflow.contrib.learn.python.learn.estimators import dnn_linear_combined
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/learn/python/learn/estimators/dnn_linear_combined.py", line 36, in <module>
    from tensorflow.contrib.learn.python.learn.estimators import estimator
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/learn/python/learn/estimators/estimator.py", line 52, in <module>
    from tensorflow.contrib.learn.python.learn.learn_io import data_feeder
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/learn/python/learn/learn_io/__init__.py", line 26, in <module>
    from tensorflow.contrib.learn.python.learn.learn_io.dask_io import extract_dask_data
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/contrib/learn/python/learn/learn_io/dask_io.py", line 33, in <module>
    import dask.dataframe as dd
  File "/usr/local/lib/python3.5/dist-packages/dask/dataframe/__init__.py", line 3, in <module>
    from .core import (DataFrame, Series, Index, _Frame, map_partitions,
  File "/usr/local/lib/python3.5/dist-packages/dask/dataframe/core.py", line 20, in <module>
    from .. import array as da
  File "/usr/local/lib/python3.5/dist-packages/dask/array/__init__.py", line 4, in <module>
    from .core import (Array, block, concatenate, stack, from_array, store,
  File "/usr/local/lib/python3.5/dist-packages/dask/array/core.py", line 50, in <module>
    from ..bytes.core import get_mapper, get_fs_token_paths
  File "/usr/local/lib/python3.5/dist-packages/dask/bytes/__init__.py", line 4, in <module>
    from .core import read_bytes, open_files, open_text_files
  File "/usr/local/lib/python3.5/dist-packages/dask/bytes/core.py", line 10, in <module>
    from .compression import seekable_files, files as compress_files
  File "/usr/local/lib/python3.5/dist-packages/dask/bytes/compression.py", line 31, in <module>
    import snappy
  File "/usr/local/lib/python3.5/dist-packages/snappy/__init__.py", line 7, in <module>
    from .SnapPy import (AbelianGroup, HolonomyGroup, FundamentalGroup,
  File "cython/core/basic.pyx", line 45, in init SnapPy
  File "/usr/local/lib/python3.5/dist-packages/snappy/horoviewer.py", line 3, in <module>
    from .CyOpenGL import *
  File "opengl/CyOpenGL.pyx", line 36, in init CyOpenGL
AttributeError: type object 'CyOpenGL.vector3' has no attribute '__reduce_cython__'
```

I can't figure out how did it happen, but I found there is a workaround to fix it, that is using `tf.layers.dense` which is the same with `tf.contrib.layers.fully_connected`. `tf.layers` is much stable than `tf.contrib.layers`.

Reference:

* [Are tf.layers.dense() and tf.contrib.layers.fully_connected() interchangeable?](https://stackoverflow.com/questions/44912297/are-tf-layers-dense-and-tf-contrib-layers-fully-connected-interchangeable)

