---
categories:
  - ucore实验
share: true
tags:
  - 操作系统
title: ucore实验环境搭建
date: 2023-11-25 19:33:53
update: 2023-11-25 20:04:15
---

## 操作系统

本次实验环境的搭建使用的是 `ubuntu` 系统，具体版本信息如下：

![](/images/IMG-ucore实验环境搭建-20231125200343190.png)
## 源码和文档

实验的源码可以从 [官方仓库](https://github.com/chyyuu/os_kernel_lab) 获取，需要注意的是目前实验所用的代码已经改为 `Rust` 语言，如果想要 `C` 语言的版本，需要切换到 `x86-32` 分支。

![](/images/IMG-ucore实验环境搭建-20231125200343210.png)

下载之后可以看到目录结构如下，其中 `labcodes` 为实验所用的源码，`labcodes_answer` 为实验的参考答案，遇到不会做的题目可以进行参考。

![](/images/IMG-ucore实验环境搭建-20231125200343242.png)

 实验的官方手册为：[ucore实验操作手册](https://github.com/chyyuu/ucore_os_docs) 包含了实验内容以及实验相关的一些拓展知识。

## GCC 安装

根据官方文档，安装 `gcc` 之后还需要再安装相 `gcc` 编译时所需的依赖，不过这些在 `ubuntu` 里安装起来很容易，两条命令就可搞定。

```bash
sudo apt-get install gcc
sudo apt-get install build-essential
```

![](/images/IMG-ucore实验环境搭建-20231125200343270.png)

![](/images/IMG-ucore实验环境搭建-20231125200343298.png)
## QEMU 安裝

文档中安装 `QEMU` 使用的命令如下：

```
sudo apt-get install qemu-system
```

![](/images/IMG-ucore实验环境搭建-20231125200343345.png)

它会安装很多程序，总共有 600M，而我们在实验中只用到 `qemu-system-i386`，所以可以只安装该程序：

```
sudo apt-get install qemu-system-i386
```

切换到 `labcodes_answer/lab1_result` 目录，执行 `make qemu` 命令，如果弹出 `QEMU` 程序，并开始正常执行，说明时延环境搭建成功了。

![](/images/IMG-ucore实验环境搭建-20231125200343371.png)

![](/images/IMG-ucore实验环境搭建-20231125200343394.png)

![code](ucore实验报告/code.md)