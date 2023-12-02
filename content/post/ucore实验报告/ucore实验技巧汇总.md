---
share: true
tags:
  - gdb
  - 调试
  - ucore实验
categories:
  - ucore实验
title: ucore实验技巧汇总
date: 2023-12-02 19:57:05
update: 2023-12-02 20:06:45
---


### gdb tui 界面

使用 ide 工具进行 debug 的时候可以很明显的看到当前执行的是源码的哪个文件中的哪行代码，`gdb` 提供的 `tui` 界面可以实现类型的功能，只需要执行命令的时候带上 `-tui` 参数。

![](/images/ucore实验技巧汇总_image_1.png)

下面是做 `ucore` 实验时，执行 `gdb -x gdbinit -tui` 命令后打开的一个 `gdb` 的命令行界面：

![](/images/ucore实验技巧汇总_image_2.png)