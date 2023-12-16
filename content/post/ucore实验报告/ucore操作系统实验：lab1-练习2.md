---
share: true
tags:
  - 操作系统
  - 系统启动
categories:
  - ucore实验
title: ucore操作系统实验：lab1-练习2
date: 2023-12-16 19:59:54
update: 2023-12-16 20:08:30
---

## 练习内容

![](/images/ucore操作系统实验：lab1-练习2_image_1.png)

## 问题解答

**问题 1：从 CPU 加电后执行的第一条指令开始，单步跟踪 BIOS 的执行**

在项目目录下执行 `make gdb` 命令，可以看到启动了一个 `QEMU` 虚拟机，此时它正等待着 `gdb` 远程连接：

![](/images/ucore操作系统实验：lab1-练习2_image_2.png)

接下来使用 `gdb` 命令进行调试，输入 `set architecture i8086` 设置当前调试的机器为 `i8086`，输入 `target remote : 1234` 连接到 `QEMU`：

![](/images/ucore操作系统实验：lab1-练习2_image_3.png)

此时输入 `si` 则会开始执行一条命令：

![](/images/ucore操作系统实验：lab1-练习2_image_4.png)

**问题 2：在初始化位置 0x7c00 设置实地址断点, 测试断点正常**

每次进行调试时都进行连接是比较麻烦的，可以将一些前置命令放在一个文件里，如下面的文件 `gdbinit`，每次使用 `gdb -x gdbinit` 命令启动 `gdb`，那么文件 `gdbinit` 中所用的命令都会被执行，之后都通过这种方式来执行。

![](/images/ucore操作系统实验：lab1-练习2_image_5.png)

![](/images/ucore操作系统实验：lab1-练习2_image_6.png)

在 `gdbinit` 文件中输入如下内容，再次进行调试：

```int
set architecture i8086
target remote:1234
b *0x7c00 #设置点
c     
x/10i $pc #显示汇编指令
```

![](/images/ucore操作系统实验：lab1-练习2_image_7.png)

**问题 3：从 0x7c00 开始跟踪代码运行，将单步跟踪反汇编得到的代码与 bootasm.S 和 bootblock.asm 进行比较**

`boot/bootasm.S` 为源码文件， `obj/bootblock.asm` 为 `obj/bootblock.o` 反汇编后的文件。

![](/images/ucore操作系统实验：lab1-练习2_image_8.png)

比较两个两个文件中的内容和单步跟踪的输出内容，可以看到两者是差不多的：

![](/images/ucore操作系统实验：lab1-练习2_image_9.png)


![](/images/ucore操作系统实验：lab1-练习2_image_10.png)

**问题 4：自己找一个 bootloader 或内核中的代码位置，设置断点并进行测试**

这里选择使用 `kern/init/init.c` 中的 `kern_init` 函数作为断点：

![](/images/ucore操作系统实验：lab1-练习2_image_11.png)

将 `gdbinit` 文件修改为：

```init
set architecture i8086
file bin/kernel
target remote:1234
b kern_init #设置点
c     
x/10i $pc #显示汇编指令
```

获得断点处的指令如下：

![](/images/ucore操作系统实验：lab1-练习2_image_12.png)