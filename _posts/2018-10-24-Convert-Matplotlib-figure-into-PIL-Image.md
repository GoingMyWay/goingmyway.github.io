---
title: Convert Matplotlib figure into PIL Image
date: 2018-10-24 09:03:56
tags: Matplotlib
categories: Matplotlib
---

These days, I want to use Tensorboard to show images created by Matplotlib or its counterparts. And the most important part is converting Matplotlib's figure into PIL image class in memory, after googling for a while, I got the solution, here it is

```python
import matplotlib
matplotlib.use('agg')

import PIL
import numpy as np
import seaborn as sns

from matplotlib import pyplot as PLT

data = np.random.randn(50, 20)
ax = sns.heatmap(data, xticklabels=2, yticklabels=False)
canvas = PLT.get_current_fig_manager().canvas
pil_image = PIL.Image.frombytes('RGB', canvas.get_width_height(), 
                 canvas.tostring_rgb())
```

Note that Searborn is a simple to use data visualization library built on Matplotlib, in the code above, there is a `canvas` instance which converts figure into `string_rgb` format so that it can be converted into an instance of PIL Image class for later use.

And you can easily convert `pil_image` into a numpy Array

```python
np_img = np.array(pil_image)
```


Reference

* https://stackoverflow.com/questions/3938676/python-save-matplotlib-figure-on-an-pil-image-object
