---
title: Linux 信号处理
date: 2021-07-03 12:49:03
tags:
---

之前在Linux C程序中对崩溃信号一直处理不好,偶然间发现libSegFault.so这个库,由于这个库是glibc提供的,基本常用的发行版都会自带这个库的,所以想之后程序中不在处理会导致程序崩溃的信号,统一交给libSegFault来处理

## libSegFault使用方式

```sh
env SEGFAULT_SIGNALS="segv, ill, abrt, bus" LD_PRELOAD=/lib/libSegFault.so someapp
```
SEGFAULT_SIGNALS不设置的话,默认只处理segv;设置为all,会处理segv, ill, abrt, fpe, bus, stkflt等信号。需要注意的是，想要使用libSegFault的话，程序里一定不要再通过signal/sigaction来捕获相关信号了，否则libSegFault是不会生效的。  

## 参考资料  

[stackoverflow](https://stackoverflow.com/questions/18706496/can-one-use-libsegfault-so-to-get-backtraces-for-sigabrt)
[libSegFault源码](https://sourceware.org/git/?p=glibc.git;a=blob;f=debug/segfault.c;hb=HEAD)
