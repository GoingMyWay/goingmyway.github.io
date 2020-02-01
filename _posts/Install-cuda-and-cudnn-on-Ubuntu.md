---
title: Install cuda and cudnn on Ubuntu
date: 2017-07-03 14:49:32
tags: CUDA
categories: CUDA
---

### CUDA installation
<ol>
* download the **runfile** of CUDA from [NVIDIA](https://developer.nvidia.com/cuda-downloads)
* install it follow instructions given by NVIDIA: use the **default** value given by the runfile
* add the following to `~/.bashrc`

```shell
export PATH=$PATH:/usr/local/cuda-8.0/bin

export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-8.0/lib64
```

### CUDNN installation

Download the cudnn from NVIDIA, it is a library which can boost computation speed of neural network. Untar the file and follow the following instructions

Copy `cudnn.h` in `include` to `cuda/include`

```shell
$ cd cuda
$ ls -l
total 8
drwxrwxr-x 2 doom doom 4096 May 29 21:19 include
drwxrwxr-x 2 doom doom 4096 May 29 21:19 lib64
$ cd include
$ cp cudnn.h /usr/local/cuda/include/</pre>
Copy lib files to <code>cuda/lib64</code>
$ ls -l
total 150908
lrwxrwxrwx 1 doom doom       13 Nov  7  2016 libcudnn.so -> libcudnn.so.5
lrwxrwxrwx 1 doom doom       18 Nov  7  2016 libcudnn.so.5 -> libcudnn.so.5.1.10
-rwxr-xr-x 1 doom doom 84163560 Nov  7  2016 libcudnn.so.5.1.10
-rw-r--r-- 1 doom doom 70364814 Nov  7  2016 libcudnn_static.a</pre>
```

Note that you don't need to copy the link files

```shell
$ cp libcudnn.so.5.1.10 /usr/local/cuda/lib64/
$ cp libcudnn_static.a /usr/local/cuda/lib64/
```

Make link files

```shell
$ cd /usr/local/cuda/lib64/
$ sudo ln -s libcudnn.so.5.1.10 libcudnn.so.5
$ sudo ln -s libcudnn.so.5 libcudnn.so</pre>
```

check the links files

```shell
$ ls -l libcudnn*
lrwxrwxrwx 1 root root       13 May 29 15:18 libcudnn.so -> libcudnn.so.5
lrwxrwxrwx 1 root root       18 May 29 15:18 libcudnn.so.5 -> libcudnn.so.5.1.10
-rwxr-xr-x 1 root root 84163560 May 29 15:17 libcudnn.so.5.1.10
-rw-r--r-- 1 root root 70364814 May 29 15:17 libcudnn_static.a</pre>
```

### Check Installation

After installation, you should check whether you have successfully installed CUDA. To check that, compile the samples in CUDA home

```shell
$ cd /usr/local/cuda/samples
$ sudo make
```

After compiling, run `deviceQuery` in `bin/x86_64/linux/release`

```shell
$ cd bin/x86_64/linux/release
$ ./deviceQuery
./deviceQuery
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 4 CUDA Capable device(s)

Device 0: "GeForce GTX TITAN X"
  CUDA Driver Version / Runtime Version          8.0 / 8.0
  CUDA Capability Major/Minor version number:    5.2
  Total amount of global memory:                 12205 MBytes (12798197760 bytes)
  (24) Multiprocessors, (128) CUDA Cores/MP:     3072 CUDA Cores
  GPU Max Clock rate:                            1076 MHz (1.08 GHz)
  Memory Clock rate:                             3505 Mhz
  Memory Bus Width:                              384-bit
  L2 Cache Size:                                 3145728 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
  Run time limit on kernels:                     No
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 2 / 0
  Compute Mode:
     Default (multiple host threads can use ::cudaSetDevice() with device simultaneously)

Device 1: "GeForce GTX TITAN X"
  CUDA Driver Version / Runtime Version          8.0 / 8.0
  CUDA Capability Major/Minor version number:    5.2
  Total amount of global memory:                 12207 MBytes (12799574016 bytes)
  (24) Multiprocessors, (128) CUDA Cores/MP:     3072 CUDA Cores
  GPU Max Clock rate:                            1076 MHz (1.08 GHz)
  Memory Clock rate:                             3505 Mhz
  Memory Bus Width:                              384-bit
  L2 Cache Size:                                 3145728 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
  Run time limit on kernels:                     No
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 3 / 0
  Compute Mode:
     Default (multiple host threads can use ::cudaSetDevice() with device simultaneously)

Device 2: "GeForce GTX TITAN X"
  CUDA Driver Version / Runtime Version          8.0 / 8.0
  CUDA Capability Major/Minor version number:    5.2
  Total amount of global memory:                 12207 MBytes (12799574016 bytes)
  (24) Multiprocessors, (128) CUDA Cores/MP:     3072 CUDA Cores
  GPU Max Clock rate:                            1076 MHz (1.08 GHz)
  Memory Clock rate:                             3505 Mhz
  Memory Bus Width:                              384-bit
  L2 Cache Size:                                 3145728 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
  Run time limit on kernels:                     No
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 131 / 0
  Compute Mode:
      Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) 

Device 3: "GeForce GTX TITAN X"
  CUDA Driver Version / Runtime Version          8.0 / 8.0
  CUDA Capability Major/Minor version number:    5.2
  Total amount of global memory:                 12207 MBytes (12799574016 bytes)
  (24) Multiprocessors, (128) CUDA Cores/MP:     3072 CUDA Cores
  GPU Max Clock rate:                            1076 MHz (1.08 GHz)
  Memory Clock rate:                             3505 Mhz
  Memory Bus Width:                              384-bit
  L2 Cache Size:                                 3145728 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
  Run time limit on kernels:                     No
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 132 / 0
  Compute Mode:
        Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >  ;
     Peer access from GeForce GTX TITAN X (GPU0) ->; GeForce GTX TITAN X (GPU1) : Yes
     Peer access from GeForce GTX TITAN X (GPU0) ->; GeForce GTX TITAN X (GPU2) : No
     Peer access from GeForce GTX TITAN X (GPU0) ->; GeForce GTX TITAN X (GPU3) : No
     Peer access from GeForce GTX TITAN X (GPU1) ->; GeForce GTX TITAN X (GPU0) : Yes
     Peer access from GeForce GTX TITAN X (GPU1) ->; GeForce GTX TITAN X (GPU2) : No
     Peer access from GeForce GTX TITAN X (GPU1) ->; GeForce GTX TITAN X (GPU3) : No
     Peer access from GeForce GTX TITAN X (GPU2) ->; GeForce GTX TITAN X (GPU0) : No
     Peer access from GeForce GTX TITAN X (GPU2) ->; GeForce GTX TITAN X (GPU1) : No
     Peer access from GeForce GTX TITAN X (GPU2) ->; GeForce GTX TITAN X (GPU3) : Yes
     Peer access from GeForce GTX TITAN X (GPU3) ->; GeForce GTX TITAN X (GPU0) : No
     Peer access from GeForce GTX TITAN X (GPU3) ->; GeForce GTX TITAN X (GPU1) : No
     Peer access from GeForce GTX TITAN X (GPU3) ->; GeForce GTX TITAN X (GPU2) : Yes

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 8.0, CUDA Runtime Version = 8.0, NumDevs = 4, Device0 = GeForce GTX TITAN X, Device1 = GeForce GTX TITAN X, Device2 = GeForce GTX TITAN X, Device3 = GeForce GTX TITAN X
Result = PASS
```

If you see all the informations on GPU, it means that you have successfully installed CUDA+CUDNN
