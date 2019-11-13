# 第三章：中断

## 本章概要

在CPU一条接着一条执行指令的过程中，有时会遇到一些突发情况，不得不停下来，跳转到对应处理函数进行处理，处理结束后再回到原来的地方继续执行指令。

> **[info] 中断分类**
> 
> **异常(Exception)**，指在执行一条指令的过程中发生了错误，此时我们通过中断来处理错误。最常见的异常包括：访问无效内存地址、执行非法指令(除零)、发生缺页等。他们有的可以恢复(如缺页)，有的不可恢复(如除零)，只能终止程序执行。
> 
> **陷入(Trap)**，指我们主动通过一条指令停下来，并跳转到处理函数。常见的形式有通过``ecall``进行**系统调用(syscall)**，或通过``ebreak``进入**断点(breakpoint)**。
> 
> **外部中断(Interrupt)**，简称中断，指的是CPU的执行过程被外设发来的信号打断，此时我们必须先停下来对该外设进行处理。典型的有定时器倒计时结束、串口收到数据等。
> 
> 外部中断是**异步(asynchronous)**的，CPU并不知道外部中断将何时发生。CPU也并不需要一直在原地等着外部中断的发生，而是执行代码，有了外部中断才去处理。我们知道，CPU的主频远高于I/O设备，这样避免了CPU资源的浪费。
> 

本章你将会学到：

* riscv 的中断相关知识
* 中断前后如何进行上下文环境的保存与恢复
* 处理最简单的断点中断和时钟中断。

代码可以在[这里]()找到。






