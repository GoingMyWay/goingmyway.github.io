---
title: TensorFlow GPU allow growth failed
date: 2020-02-19 11:39:53
tags: TensorFlow
categories: TensorFlow
---

Normally, when you use TensorFlow on GPUs, you do not need the whole chunk GPU memory, so we can allow the GPU usage to growth when we need more by

```python
tf_config = tf.ConfigProto()
tf_config.gpu_options.allow_growth = True
return tf.Session(config=tf_config)
```

However, it may fail for some reasons, so forcing the `tf_config.gpu_options.allow_growth` to work by

```python
os.environ['TF_FORCE_GPU_ALLOW_GROWTH'] = 'true'
```

Reference: https://stackoverflow.com/questions/47910681/tensorflow-setting-allow-growth-to-true-does-still-allocate-memory-of-all-my-gp
