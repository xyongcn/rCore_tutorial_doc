## **_最新通知_**

由于本文档还不稳定，有时会有更新，更新信息会第一时间放在这里。由于文档不稳定引起的问题不会导致扣分。

> **[info] 最后更新日期：2020-03-05**
>
> **2020-03-05**
>
> 为了显得很轻量级，在首页更新了目前的总代码行数。
>
> 正文方面：新增了第九章第四小节作为练习八的基础,同时在第九章 intro 部分上传了 rCore 和 xv6 文件系统的分析文档。
>
> 练习方面：
>
> 在练习五的描述中，将 `sys_fork` 的 syscall id 设定为 $$220$$；
>
> 在联系六中增加了测试文件需要用到的 syscall id；
>
> 重写了练习八，新增了练习八的测试程序。
>
> **2020-03-04**
>
> 调换了练习五和练习六的顺序。
>
> 修改了练习八的要求，强制要求实现 `sys_fork` 。
>
> 在 `exercise/introduction` 中增加了测评的详细说明。
>
> 删除了从零开始复现的要求，只对练习进行检察。
>
> **2020-03-03**
>
> 更新了第五章第一节的小节部分以及第二节的前半部分，指出了必要的链接脚本的改动，进行了更加流畅的衔接；
>
> 更新了第九章第一、二小节，使得记事本和用户终端两个应用程序支持退格键。
>
> **2020-03-02**
>
> 更新了实验报告的命名要求与放置位置。
>
> **2020-02-27**
>
> 修改了 `2. 物理内存管理` 章节中的 `实验要求 2（问答题）`。
>
> 优化了 `1. 中断异常` 章节中的 `实验要求 3（问答题）` 的描述。
>
> **2020-02-26**
>
> 简化了 `5. CPU 调度` 章节中的测试用例，删掉了对 `sys_wait` 等系统调用的要求，并且降低了对输出数据的的要求。
>
> **2020-02-20**
>
> 如果在编译 _buddy_system_allocator_ 时报错，可能是本地 crate 版本未更新，只需进入 _os/,usr/_ 文件夹下分别 `cargo update -p buddy_system_allocator` ，并重新编译即可。
>
> 如果内核在输出 `setup process!` 后 panic 报 page fault ，则很有可能将 `timer::init` 函数中的 `TICKS = 0;` 注释掉即可正常运行。

# rCore Tutorial

这是一个展示如何从零开始用 Rust 语言写一个基于 64 位 RISC-V 架构的操作系统的教程。完成这个教程后，你将可以在内核上运行用户态终端，并在终端内输入命令运行其他程序。

我们很轻量级！截至目前的代码行数分布(ch9-pa4 分支)为：

```
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Rust                            42            315             21           2178
D                              120            256              0            633
Assembly                         4             16              2            185
JSON                           116              0              0            116
Markdown                         1              4              0             55
make                             2             17              0             54
TOML                             2              5              2             22
Bourne Shell                     1              0              0              1
-------------------------------------------------------------------------------
SUM:                           288            613             25           3244
-------------------------------------------------------------------------------
```

## 代码仓库

左侧章节目录中含有一对方括号"[ ]"的小节表示这是一个存档点，即这一节要对最近几节的代码进行测试。所以我们对每个存档点都设置了一个 commit 保存其完整的状态以供出现问题时参考。

与章节相对应的代码可以很容易的找到。章节标题下提供了指向下一个存档点代码状态的链接。

## 阅读在线文档并进行实验

- [实验 ppt：rcore step-by-step tutorial](https://rcore-os.github.io/rCore_tutorial_doc/os2atc2019/os2atc.html)
- [实验文档：rcore step-by-step tutorial](https://rcore-os.github.io/rCore_tutorial_doc/)
- [实验代码：rcore step-by-step code](https://github.com/rcore-os/rCore_tutorial/)

## 评论区

对于章节内容有任何疑问及建议，请在对应页面最下面的评论区中发表观点。注意需要用 Github ID 登录后才能评论。

##

好了，那就让我们正式开始！
