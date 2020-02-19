---
title: nvidia-smi free GPU memory
date: 2020-02-19 16:19:53
tags: nvidia
categories: nvidia
---

When you programs exit, the GPU memory cannot be freed at times, so manually free the GPU memory by killing some processes.

First, check processes that are still taking the GPU memory

```bash
$ fuser -v /dev/nvidia*

                     USER        PID  ACCESS COMMAND
/dev/nvidia0:        root       1256  F...m  Xorg
                     username   2057  F...m  compiz
                     username   2759  F...m  chrome
                     username   2777  F...m  chrome
                     username   20450 F...m  python
                     username   20699 F...m  python
```
Then, kill them

```bash
$ kill -9 THE_PID_YOU_WANT_TO_KILL
```


Done!


Reference: [https://stackoverflow.com/questions/15197286/how-can-i-flush-gpu-memory-using-cuda-physical-reset-is-unavailable/46597252](https://stackoverflow.com/questions/15197286/how-can-i-flush-gpu-memory-using-cuda-physical-reset-is-unavailable/46597252)
