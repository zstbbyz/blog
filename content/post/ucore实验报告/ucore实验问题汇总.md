---
share: true
tags:
  - 操作系统
categories:
  - ucore实验
date: 2023-11-25 19:47:32
update: 2023-11-25 20:01:52
title: ucore实验问题汇总
---


##### 问题 1：lab1 编译时出现 `obj/bootbloc.out' size: 600 bytes` 

**问题描述**

在进行 lab1 的过程中，发现源码中提供的答案也无法通过编译，并提示如下内容：

![](/images/IMG-ucore实验问题汇总-20231125200216789.png)

**解决方案一**

从源码仓库的 `issues` 中看到有类似的问题：[ubuntu18中 lab1 编译过程中 bootblock文件大小600B，无法继续编译 · Issue #50 · chyyuu/os_kernel_lab (github.com)](https://github.com/chyyuu/os_kernel_lab/issues/50)

![](/images/IMG-ucore实验问题汇总-20231125200216808.png)

![](/images/IMG-ucore实验问题汇总-20231125200216840.png)

具体原因为高版本的 `gcc` 编译之后的文件过大，解决方案是使用低版本的 `gcc`。

**解决方案二**

 `lab2_result` 在不降低 `gcc` 版本的情况下是可以编译成功的，所有对比与 `bootblock` 相关的文件，发现在 `bootmian.c` 中有两行不同，进行修改后可以编译成功。

![](/images/IMG-ucore实验问题汇总-20231125200216865.png)