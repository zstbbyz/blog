---
share: true
tags:
  - 操作系统
categories:
  - ucore实验
title: ucore操作系统实验：lab1
date: 2023-12-02 17:23:18
update: 2023-12-03 22:32:15
---

## 练习 1：理解通过 make 生成执行文件的过程

### 练习内容

![](/images/ucore操作系统实验：lab1_image_1.png)

### 问题解答

**问题 1：操作系统镜像文件 ucore. img 是如何一步一步生成的？**

实验源码的目录结构如下，我们切换到 `ucore_lab/labcodes_answer/lab1_result` 目录下执行两条命令：
- `make clean` 清除掉上一次生成的文件
- `make V=` 编译文件生成镜像

![](/images/ucore操作系统实验：lab1_image_2.png)

![](/images/ucore操作系统实验：lab1_image_3.png)

执行 `make V=` 的过程中全部输出如下，它显示了整个过程中执行的所有命令：

```sh
+ cc kern/init/init.c
gcc -Ikern/init/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/init/init.c -o obj/kern/init/init.o
+ cc kern/libs/readline.c
gcc -Ikern/libs/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/libs/readline.c -o obj/kern/libs/readline.o
+ cc kern/libs/stdio.c
gcc -Ikern/libs/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/libs/stdio.c -o obj/kern/libs/stdio.o
+ cc kern/debug/kdebug.c
gcc -Ikern/debug/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/debug/kdebug.c -o obj/kern/debug/kdebug.o
+ cc kern/debug/kmonitor.c
gcc -Ikern/debug/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/debug/kmonitor.c -o obj/kern/debug/kmonitor.o
+ cc kern/debug/panic.c
gcc -Ikern/debug/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/debug/panic.c -o obj/kern/debug/panic.o
+ cc kern/driver/clock.c
gcc -Ikern/driver/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/driver/clock.c -o obj/kern/driver/clock.o
+ cc kern/driver/console.c
gcc -Ikern/driver/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/driver/console.c -o obj/kern/driver/console.o
+ cc kern/driver/intr.c
gcc -Ikern/driver/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/driver/intr.c -o obj/kern/driver/intr.o
+ cc kern/driver/picirq.c
gcc -Ikern/driver/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/driver/picirq.c -o obj/kern/driver/picirq.o
+ cc kern/trap/trap.c
gcc -Ikern/trap/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/trap/trap.c -o obj/kern/trap/trap.o
+ cc kern/trap/trapentry.S
gcc -Ikern/trap/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/trap/trapentry.S -o obj/kern/trap/trapentry.o
+ cc kern/trap/vectors.S
gcc -Ikern/trap/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/trap/vectors.S -o obj/kern/trap/vectors.o
+ cc kern/mm/pmm.c
gcc -Ikern/mm/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/mm/pmm.c -o obj/kern/mm/pmm.o
+ cc libs/printfmt.c
gcc -Ilibs/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/  -c libs/printfmt.c -o obj/libs/printfmt.o
+ cc libs/string.c
gcc -Ilibs/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/  -c libs/string.c -o obj/libs/string.o
+ ld bin/kernel
ld -m    elf_i386 -nostdlib -T tools/kernel.ld -o bin/kernel  obj/kern/init/init.o obj/kern/libs/readline.o obj/kern/libs/stdio.o obj/kern/debug/kdebug.o obj/kern/debug/kmonitor.o obj/kern/debug/panic.o obj/kern/driver/clock.o obj/kern/driver/console.o obj/kern/driver/intr.o obj/kern/driver/picirq.o obj/kern/trap/trap.o obj/kern/trap/trapentry.o obj/kern/trap/vectors.o obj/kern/mm/pmm.o  obj/libs/printfmt.o obj/libs/string.o
+ cc boot/bootasm.S
gcc -Iboot/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Os -nostdinc -c boot/bootasm.S -o obj/boot/bootasm.o
+ cc boot/bootmain.c
gcc -Iboot/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Os -nostdinc -c boot/bootmain.c -o obj/boot/bootmain.o
+ cc tools/sign.c
gcc -Itools/ -g -Wall -O2 -c tools/sign.c -o obj/sign/tools/sign.o
gcc -g -Wall -O2 obj/sign/tools/sign.o -o bin/sign
+ ld bin/bootblock
ld -m    elf_i386 -nostdlib -N -e start -Ttext 0x7C00 obj/boot/bootasm.o obj/boot/bootmain.o -o obj/bootblock.o
'obj/bootblock.out' size: 488 bytes
build 512 bytes boot sector: 'bin/bootblock' success!
dd if=/dev/zero of=bin/ucore.img count=10000
10000+0 records in
10000+0 records out
5120000 bytes (5.1 MB) copied, 0.0234475 s, 218 MB/s
dd if=bin/bootblock of=bin/ucore.img conv=notrunc
1+0 records in
1+0 records out
512 bytes (512 B) copied, 0.000192811 s, 2.7 MB/s
dd if=bin/kernel of=bin/ucore.img seek=1 conv=notrunc
146+1 records in
146+1 records out
74923 bytes (75 kB) copied, 0.000295907 s, 253 MB/s

```

根据上述的输出结果我么可以得知，在镜像生成的整个过程中主要分为三步：

- 编译源码：`gcc` 命令的会对源码进行编译，如下面的命令将 `kern/init/init.c` 编译成目标文件 `obj/kern/init/init.o`：

    ```bash
    + cc kern/init/init.c
    gcc -Ikern/init/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/init/init.c -o obj/kern/init/init.o
    ```

- 生成可执行文件：`ld` 命令将生成的目标文件进行链接生成执行文件，如下面的命令将 `obj/kern` 目录下的目标文件连接生成可执行文件 `bin/kernel`：

    ```bash
    + ld bin/kernel
    ld -m    elf_i386 -nostdlib -T tools/kernel.ld -o bin/kernel  obj/kern/init/init.o obj/kern/libs/readline.o obj/kern/libs/stdio.o obj/kern/debug/kdebug.o obj/kern/debug/kmonitor.o obj/kern/debug/panic.o obj/kern/driver/clock.o obj/kern/driver/console.o obj/kern/driver/intr.o obj/kern/driver/picirq.o obj/kern/trap/trap.o obj/kern/trap/trapentry.o obj/kern/trap/vectors.o obj/kern/mm/pmm.o  obj/libs/printfmt.o obj/libs/string.o
    ```

- 生成镜像文件：`dd` 命令的作用是用指定大小的块拷贝一个文件，并在拷贝的同时进行指定的转换，下面的命令会创建一个 `bin/ucore.img` 文件，并将之前生成的 `bin/bootblock` 和 `bin/kernel` 拷贝到 `bin/ucore.img` 文件中。

    ```bash
    dd if=/dev/zero of=bin/ucore.img count=10000
    10000+0 records in
    10000+0 records out
    5120000 bytes (5.1 MB) copied, 0.0234475 s, 218 MB/s
    dd if=bin/bootblock of=bin/ucore.img conv=notrunc
    1+0 records in
    1+0 records out
    512 bytes (512 B) copied, 0.000192811 s, 2.7 MB/s
    dd if=bin/kernel of=bin/ucore.img seek=1 conv=notrunc
    146+1 records in
    146+1 records out
    74923 bytes (75 kB) copied, 0.000295907 s, 253 MB/s
    ```

**问题 2：一个被系统认为是符合规范的硬盘主引导扇区的特征是什么？**

引导扇区的大小为 512 字节，位于磁盘的第一个扇区，但是不是所有的磁盘都装有操作系统，所以统一规定将这 512 个字节的最后两个字节设置为标志位，取固定值 `0x55` 和 `0xAA`。

![](/images/ucore操作系统实验：lab1_image_4.png)

从实验文档中可以得知，`bin/sign` 是用来生成硬盘主引导扇区的程序，如果想从 `make` 的输出内容中看到这一步骤，可以对 `Makefile` 文件中 `bootblock` 部分进行修改。

![](/images/ucore操作系统实验：lab1_image_5.png)

修改后的内容如下：

![](/images/ucore操作系统实验：lab1_image_6.png)

这时候在执行 `make "V="` 命令，可以在输出看到多出了一部分内容，其中 `bin/sign obj/bootblock.out bin/bootblock` 就是利用 `bin/sign` 来构造引导扇区。

![](/images/ucore操作系统实验：lab1_image_7.png)

`bin/sign` 对应的源码位于 `tools/sigh.c` ，内容如下：

```c
#include <stdio.h>
#include <errno.h>
#include <string.h>
#include <sys/stat.h>

int
main(int argc, char *argv[]) {
    struct stat st;
    if (argc != 3) {
        fprintf(stderr, "Usage: <input filename> <output filename>\n");
        return -1;
    }
    if (stat(argv[1], &st) != 0) {
        fprintf(stderr, "Error opening file '%s': %s\n", argv[1], strerror(errno));
        return -1;
    }
    printf("'%s' size: %lld bytes\n", argv[1], (long long)st.st_size);
    if (st.st_size > 510) {
        fprintf(stderr, "%lld >> 510!!\n", (long long)st.st_size);
        return -1;
    }
    char buf[512];
    memset(buf, 0, sizeof(buf));
    FILE *ifp = fopen(argv[1], "rb");
    int size = fread(buf, 1, st.st_size, ifp);
    if (size != st.st_size) {
        fprintf(stderr, "read '%s' error, size is %d.\n", argv[1], size);
        return -1;
    }
    fclose(ifp);
    buf[510] = 0x55;
    buf[511] = 0xAA;
    FILE *ofp = fopen(argv[2], "wb+");
    size = fwrite(buf, 1, 512, ofp);
    if (size != 512) {
        fprintf(stderr, "write '%s' error, size is %d.\n", argv[2], size);
        return -1;
    }
    fclose(ofp);
    printf("build 512 bytes boot sector: '%s' success!\n", argv[2]);
    return 0;
}
```

从源码中可以看到将 512 个字节数据中的最后两个字节分别设置为了 `0x55` 和 `0xAA`。

```c
buf[510] = 0x55;
buf[511] = 0xAA;
```

## 练习 2：使用 qemu 执行并调试 lab1 中的软件

### 练习内容

![](/images/ucore操作系统实验：lab1_image_8.png)

### 问题解答

**问题 1：从 CPU 加电后执行的第一条指令开始，单步跟踪 BIOS 的执行**

在项目目录下执行 `make gdb` 命令，可以看到启动了一个 `QEMU` 虚拟机，此时它正等待着 `gdb` 远程连接：

![](/images/ucore操作系统实验：lab1_image_9.png)

接下来使用 `gdb` 命令进行调试，输入 `set architecture i8086` 设置当前调试的机器为 `i8086`，输入 `target remote : 1234` 连接到 `QEMU`：

![](/images/ucore操作系统实验：lab1_image_10.png)

此时输入 `si` 则会开始执行一条命令：

![](/images/ucore操作系统实验：lab1_image_11.png)

**问题 2：在初始化位置 0x7c00 设置实地址断点, 测试断点正常**

每次进行调试时都进行连接是比较麻烦的，可以将一些前置命令放在一个文件里，如下面的文件 `gdbinit`，每次使用 `gdb -x gdbinit` 命令启动 `gdb`，那么文件 `gdbinit` 中所用的命令都会被执行，之后都通过这种方式来执行。

![](/images/ucore操作系统实验：lab1_image_12.png)

![](/images/ucore操作系统实验：lab1_image_13.png)

在 `gdbinit` 文件中输入如下内容，再次进行调试：

```int
set architecture i8086
target remote:1234
b *0x7c00 #设置点
c     
x/10i $pc #显示汇编指令
```

![](/images/ucore操作系统实验：lab1_image_14.png)

**问题 3：从 0x7c00 开始跟踪代码运行，将单步跟踪反汇编得到的代码与 bootasm.S 和 bootblock.asm 进行比较**

`boot/bootasm.S` 为源码文件， `obj/bootblock.asm` 为 `obj/bootblock.o` 反汇编后的文件。

![](/images/ucore操作系统实验：lab1_image_7.png)

比较两个两个文件中的内容和单步跟踪的输出内容，可以看到两者是差不多的：

![](/images/ucore操作系统实验：lab1_image_15.png)


![](/images/ucore操作系统实验：lab1_image_16.png)

**问题 4：自己找一个 bootloader 或内核中的代码位置，设置断点并进行测试**

这里选择使用 `kern/init/init.c` 中的 `kern_init` 函数作为断点：

![](/images/ucore操作系统实验：lab1_image_17.png)

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

![](/images/ucore操作系统实验：lab1_image_18.png)


## 练习 3：分析 bootloader 进入保护模式的过程

### 练习内容

![](/images/ucore操作系统实验：lab1_image_19.png)

### 问题解答

**问题 1：为何开启 A20，以及如何开启 A20**

**A20 问题来源**

> A20 指的是计算机中第 21 根地址总线。

早期的 intel 8086 和 intel 8088 中有 20 根地址总线，理论上可以访问的地址空间大小为 $2^{20}=1M$ ,但由于该系列的 CPU 中只有 16 根数据总线，  所以实际上能够表示的地址范围仅为 0~64K 。

为了可以访问到全部的 1M 内存空间，intel 采用了如下的地址计算方式：

$$内存地址 = (段基地址 << 4) + 偏移量$$

此时可以获得的最大地址为：

$$
\begin{equation}
\begin{aligned}
最大内存地址 &= 最大段基地址 << 4 + 最大偏移量 \\
					& = FFFF << 4 + FFFF \\
                      &= FFFF0 + FFFF \\
                      &= 10FFEF \\
                      & = 1M + 64KB -16B
\end{aligned}
\end{equation}
$$

可以看到在计算地址的过程中有可能会出现地址大于 1M 的越界现象，对于这些越界的地址（ 100000~10FFEF），intel 8086 和 intel 8088 会采用 wrap-around 技术来处理，直白点讲就是将地址对 1M 进行求模。

CPU 发展到 intel 80286 时，地址总线变为了 24 根，能够访问的地址空间变为了 $2^{24}=16M$，之前的对于 intel 8086 和 intel 8088 而言的越界地址（ 100000~10FFEF），在 intel 80286 中已经不算越界了。不过为了兼容之前的 CPU，使系统表现的行为不发生变化，出现了 A20 Gate。
- 当 A20 处于关闭状态时，第 21 一根地址总线的值总是 0，此时访问地址 100000~10FFEF 实际访问到的是 0~FFEF，  表现的如同在 intel 8086 和 intel 8088 中一样；
- 当 A20 处于开启状态时，第 21 根地址总线的值既可以为 0 也可以为 1，那么就可以正常的访问 100000~10FFEF 这一段空间。  

**实模式和实模式**

实模式可以简单的理解为 Intel 80286 出现之前 CPU 的工作模式，它的特点是直接使用真实的物理地址访问内存，可使用的内存地址空间为 1M，对所有可寻址内存、I/O 地址和外设硬件的访问没有限制，不支持内存保护、多任务处理和特权级等。保护模式是 Intel 80286 之后出现的 CPU 的工作模式，与实模式最大区别是用逻辑地址代替了真实地址，可以采用分段存储管理机制和分页存储管理机制，不仅为存储共享和保护提供了硬件支持，而且为实现虚拟存储提供了硬件支持。同时保护模式下通过提供 4 个特权级和完善的特权检查机制，既能实现资源共享又能保证代码数据的安全及任务的隔离。

因为 Intel 80286 之后的 CPU 是向前兼容的，所以它们本身都支持实模式，目前大部分计算机启动时也都是先在实模式下运行，之后再跳转到保护模式。

**开启 A20 的原因**

计算机在启动时首先运行在实模式，为了跟早先的 CPU 兼容，实模式下 A20 都处于关闭状态，此时如果不开启 A20，那么跳转到保护模式后，能访问到的真实物理内存只有 `0-1M`, `2-3M`, `4-5M` 等奇数内存，所以想要访问完整的内存空间必须开启 A20。

**开启 A20 的方法**

根据提示阅读 `lab1/boot/bootasm.S` ，其中开启 A20 的代码如下，在 ucore 实验中通过控制键盘控制器实现 A20 的开启。

```asm
seta20.1:
    inb $0x64, %al           # 从0x64端口读取键盘控制器状态到al寄存器中
    testb $0x2, %al          # 判断al寄存器第2为是否为1，如果是执行下一条指令
    jnz seta20.1             # 跳转到seta20.1重新执行

    movb $0xd1, %al          # 设置al寄存器的值为 0xd1
    outb %al, $0x64          # 将al中的值写入0x64端口

seta20.2:
    inb $0x64, %al            # 从0x64端口读取键盘控制器状态到al寄存器中
    testb $0x2, %al           # 判断al寄存器第2为是否为1，如果是执行下一条指令
    jnz seta20.2              # 跳转到seta20.2重新执行

    movb $0xdf, %al           # 设置al寄存器的值为 0xdf
    outb %al, $0x60           # 将al中的值写入0x60端口
```

所以开启 A20 的整个步骤为：

- 向键盘控制器的 `0x64` 端口发送的命令 `0xd1`，即代码段 `seta20.1` 完成的工作；
- 向键盘控制器的 `0x60` 端口发送的命令 `0xdf`，即代码段 `seta20.2` 完成的工作；

**问题 2：如何初始化 GDT 表**

ucore 在 `lab1/boot/bootasm.S` 文件尾部定义 GDT 表，代码如下：

```asm
# Bootstrap GDT
.p2align 2                                  # force 4 byte alignment
gdt:
    SEG_NULLASM                             # null seg
    SEG_ASM(STA_X|STA_R, 0x0, 0xffffffff)   # code seg for bootloader and kernel
    SEG_ASM(STA_W, 0x0, 0xffffffff)         # data seg for bootloader and kernel

gdtdesc:
    .word 0x17                              # sizeof(gdt) - 1
    .long gdt                               # address gdt
```

其中 `gdt` 为 ucore 中构造出的 GDT ，`gdtdesc` 记录了 GDT 的长度和内存地址，在 `lab1/boot/bootasm.S` 中有如下这么一条指令，它的作用是将 `gdtdesc` 处的数据读取到全局描述符表寄存器 GDTR 中。

```asm
lgdt gdtdesc
```


**问题 3：如何使能和进入保护模式**

在 CPU 中有一个 `CR0` 寄存器，包含了 6 个预定义标志，第 0 位是保护允许位 PE ( Protedted Enable )，用于启动保护模式，如果 PE 位置 1，则保护模式启动，如果 PE=0，则在实模式下运行。所以启动保护模式只需要将 `CR0` 寄存器第 0 位设为 1 即可，相关代码如下：

```asm
movl %cr0, %eax
orl $CR0_PE_ON, %eax
movl %eax, %cr0
```


## 练习 4：分析 bootloader 加载 ELF 格式的 OS 的过程

### 练习内容

![](/images/ucore操作系统实验：lab1_image_20.png)

### 问题解答

**问题 1：bootloader 如何读取硬盘扇区的**

`bootmain.c` 中有如下代码片段，作用就是从磁盘中读取扇区，整个流程大致为：

- 等待磁盘准备好
- 发出读取扇区的命令
- 等待磁盘准备好
- 把磁盘扇区数据读到指定内存

```c

// 不断的读取磁盘状态，等待磁盘准备好
static void waitdisk(void)
{
    while ((inb(0x1F7) & 0xC0) != 0x40)
}

// 读取secno处一个扇区到dst处
static void readsect(void *dst, uint32_t secno)
{
    // 等待磁盘准备好
    waitdisk();

    // 像磁盘中的寄存器写入要读取的扇区总数，这里始终为1
    outb(0x1F2, 1);

    // 写入secno
    outb(0x1F3, secno & 0xFF);
    outb(0x1F4, (secno >> 8) & 0xFF);
    outb(0x1F5, (secno >> 16) & 0xFF);
    outb(0x1F6, ((secno >> 24) & 0xF) | 0xE0);

    // 发起读命令
    outb(0x1F7, 0x20); // cmd 0x20 - read sectors

    // 等待磁盘准备好
    waitdisk();

    // 读取数据
    insl(0x1F0, dst, SECTSIZE / 4);
}
```

**问题 2：bootloader 是如何加载 ELF 格式的 OS**

下面是 `bootloader` 中加载 os 的代码，主要步骤是将 ELF 文件头部读到内存中，根据头部获取其他段的位置和长度，并读取到内存指定位置，之后开始执行入口函数，操作系统正式被运行起来。

```c
void bootmain(void)
{
    // 将操作系统第一页读取到内存中，位置在ELFHDR处,
    // SECTSIZE * 8 其中 SECTSIZE 大小为512字节一个扇区，8个扇区组成一页
    readseg((uintptr_t)ELFHDR, SECTSIZE * 8, 0);

    // 判断读取到的数据是否为一个合法的ELF，主要根据ELF头部判断
    if (ELFHDR->e_magic != ELF_MAGIC)
    {
        goto bad;
    }

    struct proghdr *ph, *eph;

    // 根据ELF头部的信息，将剩余部分读到内存中
    ph = (struct proghdr *)((uintptr_t)ELFHDR + ELFHDR->e_phoff);
    eph = ph + ELFHDR->e_phnum;
    for (; ph < eph; ph++)
    {
        readseg(ph->p_va & 0xFFFFFF, ph->p_memsz, ph->p_offset);
    }

    // 根据ELF头部信息，执行入口函数
    ((void (*)(void))(ELFHDR->e_entry & 0xFFFFFF))();

bad:
    outw(0x8A00, 0x8A00);
    outw(0x8A00, 0x8E00);

    /* do nothing */
    while (1)
        ;
}
```

## 练习 5：实现函数调用堆栈跟踪函数

### 练习内容

![](/images/ucore操作系统实验：lab1_image_21.png)


### 问题解答

根据输出样例，我们可以知道在 `print_stackframe` 要做的的是把遍历当前的函数栈，并打印每个栈中的 `ebp`、`eip` 和函数中的参数。

```c
void
print_stackframe(void) {
     /* LAB1 YOUR CODE : STEP 1 */
     /* (1) call read_ebp() to get the value of ebp. the type is (uint32_t);
      * (2) call read_eip() to get the value of eip. the type is (uint32_t);
      * (3) from 0 .. STACKFRAME_DEPTH
      *    (3.1) printf value of ebp, eip
      *    (3.2) (uint32_t)calling arguments [0..4] = the contents in address (uint32_t)ebp +2 [0..4]
      *    (3.3) cprintf("\n");
      *    (3.4) call print_debuginfo(eip-1) to print the C calling function name and line number, etc.
      *    (3.5) popup a calling stackframe
      *           NOTICE: the calling funciton's return addr eip  = ss:[ebp+4]
      *                   the calling funciton's ebp = ss:[ebp]
      */

    // 读取ebp和eip
    uint32_t ebp = read_ebp(), eip = read_eip();
    
    int i, j;

    // 遍历栈
    for (i = 0; ebp != 0 && i < STACKFRAME_DEPTH; i ++) {
        
        // 打印 ebp eip
        cprintf("ebp:0x%08x eip:0x%08x args:", ebp, eip);
        
        // 打应参数
        uint32_t *args = (uint32_t *)ebp + 2;
        for (j = 0; j < 4; j ++) {
            cprintf("0x%08x ", args[j]);
        }
        cprintf("\n");
        print_debuginfo(eip - 1);

        // 切换栈信息, 需要注意的是栈是由高地址到低地址延伸的
        eip = ((uint32_t *)ebp)[1];
        ebp = ((uint32_t *)ebp)[0];
    }
}
```


## 练习 6：完善中断初始化和处理

### 练习内容

![](/images/ucore操作系统实验：lab1_image_22.png)

### 问题解答

**问题 1：中断描述符表（也可简称为保护模式下的中断向量表）中一个表项占多少字节？其中哪几位代表中断处理代码的入口？**

ucore 里的中断描述符定义在 `kern/mm/mmu.h` 中，总共占用 64 位，即 8 字节。

```c
/* Gate descriptors for interrupts and traps */
struct gatedesc {
    unsigned gd_off_15_0 : 16;        // low 16 bits of offset in segment
    unsigned gd_ss : 16;            // segment selector
    unsigned gd_args : 5;            // # args, 0 for interrupt/trap gates
    unsigned gd_rsv1 : 3;            // reserved(should be zero I guess)
    unsigned gd_type : 4;            // type(STS_{TG,IG32,TG32})
    unsigned gd_s : 1;                // must be 0 (system)
    unsigned gd_dpl : 2;            // descriptor(meaning new) privilege level
    unsigned gd_p : 1;                // Present
    unsigned gd_off_31_16 : 16;        // high bits of offset in segment
};
```

根据代码中的注释，第 1-16 位与 48-64 位构成段偏移，第 17-32 位为段选择子，两者联合可计算出入口地址。

**问题 2：请编程完善 kern/trap/trap.c 中对中断向量表进行初始化的函数 idt_init**

```c
/* idt_init - initialize IDT to each of the entry points in kern/trap/vectors.S */

void
idt_init(void) {

     /* LAB1 YOUR CODE : STEP 2 */
     /* (1) Where are the entry addrs of each Interrupt Service Routine (ISR)?
      *     All ISR's entry addrs are stored in __vectors. where is uintptr_t __vectors[] ?
      *     __vectors[] is in kern/trap/vector.S which is produced by tools/vector.c
      *     (try "make" command in lab1, then you will find vector.S in kern/trap DIR)
      *     You can use  "extern uintptr_t __vectors[];" to define this extern variable which will be used later.
      * (2) Now you should setup the entries of ISR in Interrupt Description Table (IDT).
      *     Can you see idt[256] in this file? Yes, it's IDT! you can use SETGATE macro to setup each item of IDT
      * (3) After setup the contents of IDT, you will let CPU know where is the IDT by using 'lidt' instruction.
      *     You don't know the meaning of this instruction? just google it! and check the libs/x86.h to know more.
      *     Notice: the argument of lidt is idt_pd. try to find it!
      */

    extern uintptr_t __vectors[];
    int i;
    for (i = 0; i < sizeof(idt) / sizeof(struct gatedesc); i ++) {
        SETGATE(idt[i], 0, GD_KTEXT, __vectors[i], DPL_KERNEL);
    }

    // set for switch from user to kernel
    SETGATE(idt[T_SWITCH_TOK], 0, GD_KTEXT, __vectors[T_SWITCH_TOK], DPL_USER);

    // load the IDT
    lidt(&idt_pd);
}
```