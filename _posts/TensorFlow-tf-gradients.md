---
title: TensorFlow-tf.gradients
date: 2017-07-08 09:49:32
tags: TensorFlow
categories: TensorFlow
---

TensorFlow is such a powerful tools that you can easily to compute any value on your needs. Today I am going to introduce a function called `tf.gradients()` by which you can compute gradients. Let's go.



Before using it, let's have a look at [the docs](https://www.tensorflow.org/api_docs/python/tf/gradients)

> gradients(
>     ys,
>     xs,
>     grad_ys=None,
>     name='gradients',
>     colocate_gradients_with_ops=False,
>     gate_gradients=False,
>     aggregation_method=None
> )

And its description

> Constructs symbolic partial derivatives of sum of `ys` w.r.t. x in `xs`

> `ys` and `xs` are each a `Tensor` or a list of tensors. `grad_ys` is a list of `Tensor`, holding the gradients received by the `ys`. The list must be the same length as `ys`.
>
> `gradients()` adds ops to the graph to output the partial derivatives of `ys` with respect to `xs`. It returns a list of`Tensor` of length `len(xs)` where each tensor is the `sum(dy/dx)` for y in `ys`.
>
> `grad_ys` is a list of tensors of the same length as `ys` that holds the initial gradients for each y in `ys`. When `grad_ys` is None, we fill in a tensor of '1's of the shape of y for each y in `ys`. A user can provide their own initial `grad_ys` to compute the derivatives using a different initial gradient for each y (e.g., if one wanted to weight the gradient differently for each value in each y).



Usually, we need to calculate gradients and update the gradients and practically one can detect whether gradient vanishing or exploding are happening by summarise gradients via TensorBoard— another visulization tool developed by TensorFlow team.



Here is a simple example to clarify its usage

 Suppose you have simple linear function
$$
\widehat Y = W \times X + b
$$
And We want to fit a linear function so that we can prediction unseen data. And normally we should have a  function which in quadratic way.


$$
cost = \frac{1}{2} \times (\widehat Y-Y)^2
$$
We can get our fit by minimising the cost to a threshold for example 0.01. Here is the code to calculate gradients



```Python
In [1]: import numpy as np

In [2]: import tensorflow as tf

In [3]: sess = tf.InteractiveSession()

In [4]: X = tf.placeholder("float", shape=[2, 1])

In [5]: Y = tf.placeholder("float", shape=[2, 1])

In [6]: W = tf.Variable(np.random.randn(), name='weight')

In [7]: b = tf.Variable(np.random.randn(), name='bias')

In [8]: pred = tf.add(tf.multiply(X, W), b)

In [9]: cost = 0.5 * tf.reduce_sum(tf.pow(pred-Y, 2))

In [10]: grads = tf.gradients(cost, [W, b])

In [11]: sess.run(tf.global_variables_initializer())

In [15]: W_, b_, pred_, cost_, grads_ = sess.run([W, b, pred, cost, grads], feed_dict={X: [[2.0], [3.]], Y: [[3.0], [2.]]})

In [16]: W_, b_
Out[16]: (1.6649098, 0.54648024)

In [17]: pred_
Out[17]: 
array([[ 3.87629986],
       [ 5.5412097 ]], dtype=float32)

In [18]: cost_
Out[18]: 6.6540337

In [19]: grads_
Out[19]: [12.376228, 4.4175096]

In [20]: (3.87629986 - 3.) * 2 + (5.5412097 - 2) * 3
Out[20]: 12.376228819999998

In [21]: (3.87629986 - 3.) + (5.5412097 - 2)
Out[21]: 4.417509559999999
```

If you have learnt calculus, you can easily calculate the result 
$$
\frac {\partial cost}{\partial W} = (W \times X + b -Y) \times X
$$
and 
$$
\frac {\partial cost}{\partial b} = (W \times X +b - Y)
$$
Since the gradients are the accumlated gradients w.r.t each `x `in `xs` , to get the result, just adding all the corresponding gradients. 

Hope you can understand this post. 
