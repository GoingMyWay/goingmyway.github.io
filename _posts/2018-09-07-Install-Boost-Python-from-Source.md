---
title: Install Boost.Python from Source
date: 2018-09-07 14:21:09
tags: Boost.Python
categories: Boost.Python
---

Boost.Python is a powerful tools to build C++ bindings for Python, you can write your own libraries with C++ and create interface for Python to use. I will write some posts to introduce how to use Boost.Python. This post I will introduce steps to install Boost.Python

1  Download 

```shell
wget https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.bz2
tar -xf boost_1_67_0.tar.bz2
cd boost_1_67_0.tar.bz2
```

2  Configure

```shell
./bootstrap.sh --with-icu --with-python=/path/to/python3 --with-libraries=system,thread,python  # only install libraries related to system, thread and python
```

3  Install

```shell
./b2 && sudo ./b2 install
```

If your system is Ubuntu 18.04 64 bit, the boost.python libraries will be installed at `/usr/lib/x86_64-linux-gun/`, please check it, if not, do copy these files to this dir. Remember to make a soft link for `libbbost_python3.so` if necessary.

If you found there is a `libbost_python3x.so` already installed at `/usr/lib/x86_64-linux-gnu` you can link you program by specifying the path of the lib file. For example

```shell
PYTHON_VERSION = 3.4
PYTHON_HOME_PATH = /export/home/me/anaconda3/
PYTHON_INCLUDE = /usr/include/python3.4/

BOOST_INC = /usr/include/boost/
BOOST_LIB = /usr/lib/x86_64-linux-gnu/
BOOST_PYTHON_LIB = /usr/lib/x86_64-linux-gnu/


TARGET = libenv
EXTEND_FILE = libenv_ext

$(TARGET).so:$(TARGET).o
	g++ -shared depend.o -I$(BOOST_INC) -L$(BOOST_LIB) -L$(BOOST_PYTHON_LIB) /usr/lib/x86_64-linux-gnu/libboost_python-py34.so `python3.4-config --libs --ldflags` -o graph_ext.so
	g++ -shared depend.o $(TARGET).o -L$(BOOST_LIB) -L$(BOOST_PYTHON_LIB) /usr/lib/x86_64-linux-gnu/libboost_python-py34.so `python3.4-config --libs --ldflags` -o $(TARGET).so
	mv $(TARGET).so $(EXTEND_FILE).so

depend.o:depend.cpp
	g++ `python3.4-config --includes` -fPIC -c depend.cpp -O3 -std=c++11

$(TARGET).o:$(TARGET).cpp
	g++ `python3.4-config --includes` -fPIC -c depend.cpp $(TARGET).cpp -O3 -std=c++11

clean:
	rm *.so *.o *.gch
```

And you can use anthor Python3.x ,say 3.6, 3.7 or annaconda3 even though the lib is built with libboost_python34.so, in your computer to run you programm. Try it.
