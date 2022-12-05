---
title: cmake&gcc笔记
date: 2019-09-14 21:54:32
tags:
    - gcc
    - cmake
---

## cmake常用编译选项  

1. 指定项目名称  

    `project(myproject VERSION 0.1.0)`   
    较老版本cmake可能不支持后两个参数,可以使用`project(myproject)`  

2. 设置C++标准  

* cmake 3.1后    
    `set(CMAKE_CXX_STANDARD 11)`  
* cmake 3.1前  
    `set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")`  

3. 指定头文件路径  
    `include_directories(${PROJECT_SOURCE_DIR}/include)`  
    `include_directories(/usr/local/include/xxx)`  

4. 指定链接库路径  

    `link_directories(${PROJECT_SOURCE_DIR}/lib/)`  
    `link_directories(/usr/local/lib/xxx)`

5. 链接库  

    `link_libraries(pthread xxx.a)`  
    `link_libraries(pthread "-Wl,--whole-archive" xxx.a "-Wl,--no-whole-archive")`  

    `"-Wl,--whole-archive"`和`"-Wl,--no-whole-archive"`用于生成动态库(yyy.so),是ld使用的命令行参数  
    `"-Wl,--whole-archive"` 告诉编译器，从这里开始，所有的库的内容都包含到yyy.so中,这种方式生成的so较大,之后依赖该yyy.so的程序可以直接使用yyy.so所依赖的静态库xxx中的函数而不需要再次静态链接xxx  
    `"-Wl,--no-whole-archive"` 告诉编译器，从这里开始，以后的库的内容不用都包含到so中,so体积较小,依赖该so的程序需要使用静态库xxx中未被yyy.so使用的函数时需要再次链接xxx  

    也可以使用 `target_link_libraries(target_name "-Wl,--whole-archive" xxx.a "-Wl,--no-whole-archive" pthread)` 进行链接,`target_link_libraries`用在第7条之后,只对指定生成目标生效,`link_libraries`用在第7条之前,对之后所有生成目标均生效

6. 库与库的依赖关系

    * 动态库a依赖动态库b  

        编译a时不链接b也可以编译通过,但不要这样做  
        若a链接b,则之后生成可执行程序时不需再次链接b

    * 动态库a依赖静态库b  
        参考第五条

    *  静态库a依赖动态库b  
        编译静态库时不进行链接动作,所以a不需要链接b,a也不会包含b,之后链接a时需要同时链接b

    * 静态库a依赖静态库b  
        同上,a不需要链接b,a也不会包含b,之后链接a时需要同时链接b  
        或者可以在编译a后将a和b打包到同一个静态库中,通过命令 `add_custom_target` 完成,暂时没有研究

    * 可执行程序依赖静态库  
        必须将静态库的依赖都进行链接  

    *  可执行程序依赖动态库  
       只要编译时动态库对依赖进行了链接,此时就不再需要进行链接  

    综上所述,只有在编译可执行程序时链接是必须的,编译静态库不需要对依赖进行链接,编译动态库时不对依赖进行链接也可以编译通过(但不要这样做)

7. 生成库或可执行文件  

    `add_library(target_name SHARED ${SOURCES} ${HEADERS})`  生成动态库  
    `add_library(target_name STATIC ${SOURCES} ${HEADERS})`  生成静态库  
    `add_executable(target_name ${SOURCES} ${HEADERS})`  生成可执行程序  

8. 其他命令  

    * `set_target_properties(target_name PROPERTIES OUTPUT_NAME another_target_name)`  
    修改target_name名称为another_target_name,由于CMake中多个生成目标名称必须不同,当需要同时生成动态库和静态库时可以使用该命令同时生成相同库名的动态库和静态库  

    * GLOB添加your-folder下多个文件
    ```cmake
    file(GLOB SOURCES
            your-folder/*.hxx
            your-folder/*.cxx)
    ```

    * `aux_source_directory(. DIR_SRCS)`  

    查找当前目录下的所有源文件,并将名称保存到 DIR_SRCS 变量

9. 编译Debug版和Release版程序  

    ```cmake
    SET(CMAKE_BUILD_TYPE "Debug") 
    SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
    SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
    ```


## 参考链接  

[Linux 依赖动态库 / 静态库的动态态库 / 静态库](https://blog.csdn.net/nodeathphoenix/article/details/9982209)
