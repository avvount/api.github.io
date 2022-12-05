---
title: How to structure your project (C++)
date: 2021-07-03 12:43:12
tags:
---

怎么组织你的C++代码?之前工程目录结构一直比较混乱,查了一下C++的相关开源项目和一些资料,整理一下思路

```
.
├── bin
├── cmake
├── CMakeLists.txt
├── doc
├── extern
├── include
├── lib
├── LICENSE
├── README.md
├── src
│   └── CMakeLists.txt
└── tests
    ├── catch.hpp
    └── CMakeLists.txt
```
各个目录和文件的作用:
- cmake
  放置.cmake文件
- CMakeLists.txt
  顶层的CMakeLists.txt中设置全局配置,并通过add_subdirectory的方式添加各个子目录
- bin
  编译后的可执行程序
- lib
  编译后的动态库
- doc
  文档
- extern
  或者叫3rdparty/thirdparty,放置使用的第三方库,一般通过submodule的方式加入主工程
  工程中常用的几个第三方库,如boost、protobuf,单独编译一遍,放到子模块中,不用每个项目都重新编译
- src
  工程源代码
- include
  如果工程要对外提供头文件的话,将对外提供的头文件放到这里
  todo: 了解一下CMake的install命令
- tests
  单元测试

## 参考资料  

[github mmorse1217](https://github.com/mmorse1217/cmake-project-template)
[github kigster](https://github.com/kigster/cmake-project-template)
[cmake-basis](https://cmake-basis.github.io)
[An Introduction to Modern CMake](https://cliutils.gitlab.io/modern-cmake/)
[How do you add Boost libraries in CMakeLists.txt](https://stackoverflow.com/questions/6646405/how-do-you-add-boost-libraries-in-cmakelists-txt)