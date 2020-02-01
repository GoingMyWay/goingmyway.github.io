---
title: Understanding Session and Graph
date: 2017-07-14 11:52:33
tags: TensorFlow
Categories: TensorFlow
---

The first time when I learned TensorFlow, I was confused by Session and Graph. After Googling for a while, I knew that 

* Graph defines operations in your applicaion, it defines computation and has nothing to do with data.
* When running the Graph by session, dimensions and type of values will be checked and errors will be raised when there are some bugs in the Graph.
* To run the Graph, one must feed the data.

And Session, in my view is **Conversation**— you need a talk with the Graph and tell the Graph what you want, so in order to expel the Graph to conduct computation, you should plugin the fuel— **feed_dict** and run the Graph to get get the value you want defined in the Graph— to call `sess.run([values you want], feed_dict)`.

And if you use `with` — the conext manager in your session, every time you should initialize variables in the Graph. Multiple sessions and multiple graphs can be defined and you can use sessions to call different graphs.

```python
import tensorflow as tf

graph_1 = tf.Graph()

with graph_1.as_default():
    var = tf.Variable(100, name='var')
    init_graph_1 = tf.global_variables_initializer()
    

graph_2 = tf.Graph()

with graph_2.as_default():
    val = tf.Variable(200, name='val')
    init_graph_2 = tf.global_variables_initializer()

with tf.Session(graph=graph_1) as sess_1:
    sess_1.run(init_graph_1)
    print(sess_1.run(var))  ## output 100

```

Everytime when a session is created, one must set a graph defined before or use the defult graph. 

```python
In [7]: with tf.Session(graph=graph_1) as sess_1:
   ...:     sess_1.run(init_graph_2)
   ...:     print(sess_1.run(var))
   ...:     
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in __init__(self, fetches, contraction_fn)
    266         self._unique_fetches.append(ops.get_default_graph().as_graph_element(
--> 267             fetch, allow_tensor=True, allow_operation=True))
    268       except TypeError as e:

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/framework/ops.py in as_graph_element(self, obj, allow_tensor, allow_operation)
   2413     with self._lock:
-> 2414       return self._as_graph_element_locked(obj, allow_tensor, allow_operation)
   2415 

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/framework/ops.py in _as_graph_element_locked(self, obj, allow_tensor, allow_operation)
   2497       if obj.graph is not self:
-> 2498         raise ValueError("Operation %s is not an element of this graph." % obj)
   2499       return obj

ValueError: Operation name: "init"
op: "NoOp"
input: "^val/Assign"
 is not an element of this graph.

During handling of the above exception, another exception occurred:

ValueError                                Traceback (most recent call last)
<ipython-input-7-2147941bc790> in <module>()
      1 with tf.Session(graph=graph_1) as sess_1:
----> 2     sess_1.run(init_graph_2)
      3     print(sess_1.run(var))
      4 

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in run(self, fetches, feed_dict, options, run_metadata)
    776     try:
    777       result = self._run(None, fetches, feed_dict, options_ptr,
--> 778                          run_metadata_ptr)
    779       if run_metadata:
    780         proto_data = tf_session.TF_GetBuffer(run_metadata_ptr)

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in _run(self, handle, fetches, feed_dict, options, run_metadata)
    967 
    968     # Create a fetch handler to take care of the structure of fetches.
--> 969     fetch_handler = _FetchHandler(self._graph, fetches, feed_dict_string)
    970 
    971     # Run request and get response.

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in __init__(self, graph, fetches, feeds)
    406     """
    407     with graph.as_default():
--> 408       self._fetch_mapper = _FetchMapper.for_fetch(fetches)
    409     self._fetches = []
    410     self._targets = []

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in for_fetch(fetch)
    236         if isinstance(fetch, tensor_type):
    237           fetches, contraction_fn = fetch_fn(fetch)
--> 238           return _ElementFetchMapper(fetches, contraction_fn)
    239     # Did not find anything.
    240     raise TypeError('Fetch argument %r has invalid type %r' %

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in __init__(self, fetches, contraction_fn)
    272       except ValueError as e:
    273         raise ValueError('Fetch argument %r cannot be interpreted as a '
--> 274                          'Tensor. (%s)' % (fetch, str(e)))
    275       except KeyError as e:
    276         raise ValueError('Fetch argument %r cannot be interpreted as a '

ValueError: Fetch argument <tf.Operation 'init' type=NoOp> cannot be interpreted as a Tensor. (Operation name: "init"
op: "NoOp"
input: "^val/Assign"
 is not an element of this graph.)
```

Since the graph of  `sess_1` is `graph_1` and `init_graph_2` is defined in `graph_2`, so `sess_1` can't run `init_graph_2`. And the same as values defined in the Graphs!

```python
In [9]: with tf.Session(graph=graph_1) as sess_1:
   ...:     sess_1.run(init_graph_1)
   ...:     print(sess_1.run(val))
   ...:     
   ...:     
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in __init__(self, fetches, contraction_fn)
    266         self._unique_fetches.append(ops.get_default_graph().as_graph_element(
--> 267             fetch, allow_tensor=True, allow_operation=True))
    268       except TypeError as e:

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/framework/ops.py in as_graph_element(self, obj, allow_tensor, allow_operation)
   2413     with self._lock:
-> 2414       return self._as_graph_element_locked(obj, allow_tensor, allow_operation)
   2415 

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/framework/ops.py in _as_graph_element_locked(self, obj, allow_tensor, allow_operation)
   2492       if obj.graph is not self:
-> 2493         raise ValueError("Tensor %s is not an element of this graph." % obj)
   2494       return obj

ValueError: Tensor Tensor("val:0", shape=(), dtype=int32_ref) is not an element of this graph.

During handling of the above exception, another exception occurred:

ValueError                                Traceback (most recent call last)
<ipython-input-9-b480320eb08a> in <module>()
      1 with tf.Session(graph=graph_1) as sess_1:
      2     sess_1.run(init_graph_1)
----> 3     print(sess_1.run(val))
      4 
      5 

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in run(self, fetches, feed_dict, options, run_metadata)
    776     try:
    777       result = self._run(None, fetches, feed_dict, options_ptr,
--> 778                          run_metadata_ptr)
    779       if run_metadata:
    780         proto_data = tf_session.TF_GetBuffer(run_metadata_ptr)

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in _run(self, handle, fetches, feed_dict, options, run_metadata)
    967 
    968     # Create a fetch handler to take care of the structure of fetches.
--> 969     fetch_handler = _FetchHandler(self._graph, fetches, feed_dict_string)
    970 
    971     # Run request and get response.

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in __init__(self, graph, fetches, feeds)
    406     """
    407     with graph.as_default():
--> 408       self._fetch_mapper = _FetchMapper.for_fetch(fetches)
    409     self._fetches = []
    410     self._targets = []

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in for_fetch(fetch)
    236         if isinstance(fetch, tensor_type):
    237           fetches, contraction_fn = fetch_fn(fetch)
--> 238           return _ElementFetchMapper(fetches, contraction_fn)
    239     # Did not find anything.
    240     raise TypeError('Fetch argument %r has invalid type %r' %

/Users/qiuwei/Library/Python/3.6/lib/python/site-packages/tensorflow/python/client/session.py in __init__(self, fetches, contraction_fn)
    272       except ValueError as e:
    273         raise ValueError('Fetch argument %r cannot be interpreted as a '
--> 274                          'Tensor. (%s)' % (fetch, str(e)))
    275       except KeyError as e:
    276         raise ValueError('Fetch argument %r cannot be interpreted as a '

ValueError: Fetch argument <tf.Variable 'val:0' shape=() dtype=int32_ref> cannot be interpreted as a Tensor. (Tensor Tensor("val:0", shape=(), dtype=int32_ref) is not an element of this graph.)
```

And you can also use `InteractiveSession` to run the Graph.

```python
In [13]: inter_sess_1 = tf.InteractiveSession(graph=graph_1)

In [14]: inter_sess_1.run(init_graph_1)

In [15]: print(inter_sess_1.run(var))
100

In [16]: inter_sess_2 = tf.InteractiveSession(graph=graph_2)

In [17]: inter_sess_2.run(init_graph_2)

In [18]: print(inter_sess_2.run(val))
200
```

OK, that all my understadings. Session is a **Conversation** to communicate with the Graph, Graph is a computation paradigm!
