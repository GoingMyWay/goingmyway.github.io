---
title: How to install ViZdoom on Ubuntu
date: 2017-07-03 20:03:53
tags: ViZDoom
categories: ViZDoom
---

Let's install ViZdoom step by step

prerequisite:

* Python3.5+
* Ubuntu 14.04

After cloning the source code and f0llowing instructions given by docs of ViZdoom

Before that, you should install JDK developed by Oracle, rather than OpenJDK

```shell
sudo add-apt-repository ppa:webupd8team/java

sudo apt-get update

sudo apt-get install oracle-java8-installer

sudo apt-get install oracle-java8-set-default</pre>
```

This may take 1 or 2 hours to install, it depends on the network bandwidth.

First step: **Build**

```shell
cmake -DCMAKE_BUILD_TYPE=Release \
      -DBUILD_PYTHON3=ON -DBUILD_JAVA=ON \
      -DBUILD_LUA=ON -DPYTHON_INCLUDE_DIR=$(python3 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
      -DPYTHON_LIBRARY=$(python3 -c "import distutils.sysconfig as sysconfig; print(sysconfig.get_config_var('LIBDIR'))")
```

In this step**freedoom-0.10.1.zip** is needed, you can download it from Github 

Second step: **Make**

```shell
make
```

Copy the built Python files to site-packages path
```shell
sudo mv -f  bin/python3/pip_package/ /usr/local/lib/python3.5/site-packages/vizdoom
```

Note that you must set the correct version of Python3.5+

Then you can test it with Python3.5+. Good luck!
