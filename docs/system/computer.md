# 计算机是什么?

Wikipedia的定义如下:
> A computer is a machine that can be instructed to carry out sequences of arithmetic or logical operations automatically via computer programming. Modern computers have the ability to follow generalized sets of operations, called programs. These programs enable computers to perform an extremely wide range of tasks. A "complete" computer including the hardware, the operating system (main software), and peripheral equipment required and used for "full" operation can be referred to as a computer system. 

个人理解Computer是一个可以运行程序的电子设备, 通过CPU和相关硬件完成运算和输入输出。如果更加精确一点的话, 可以分为通用系统和专用系统, 一个系统通过硬件和软件组成, 通用系统英文叫做General Purpose System, 也就是我们一般说的Computer, 而专用系统也被翻译为嵌入式系统, 即Embedded System, 嵌入式系统需要在限定成本、
尺寸又或者特定的接口、性能下设计的硬件和软件系统。

嵌入式处理器架构大体可以分为:
- Micro Control Unit (MCU, 嵌入式微控制器, 俗称单片机)
- Digital Signal Processor (DSP, 嵌入式DSP处理器)
- Micro Processor Unit (MPU, 嵌入式微处理器)
- System on Chip (SoC, 嵌入式片上系统)
- System on a Programmable Chip (SoPC, 可编程片上系统)

其中, 我比较感兴趣的是:
- 基于 8bit/32bit microcontroller (微控制器, 比如8051, STM32) 的单片机系统
- 基于 32bit high-end embedded processor (高端嵌入式处理器, 比如rockchip RK3288) 系统, 采用Linux或Android操作系统

这里强推一下 Carrie Anne 的 [Crash Course Computer Science](https://www.bilibili.com/video/av21376839), 中文字幕, 差不多前20集可以帮助你迅速建立起对计算机的概念。


对于计算机来说, 最重要的3个组成部分是:
- CPU
- Memory
- I/O

简单来说, CPU的核心ALU(Arithmetic & Logic Unit)通过bus(总线)从ROM中读取instruction(指令), 也就是常说的fetch phase(取指令阶段),进而decode, 最后execute, 然后将执行结果写入register或RAM, 周而复始。

CPU很单纯, 但是Memory就有些麻烦, 我们用树状结构来表达: 
- System
  - CPU
  - Memory (内存, 内部存储器, 記憶體)
    - CACHE
    - Primary Memory (主存, 主存储器)
      - RAM
      - ROM
  - I/O (外部设备)
    - External Storage (外部设备)
      - Hard Drive (硬盘)
      - Flash Drive (U盘)
    - Input Device (输入设备)
      - Keyboard
      - Mouse
    - Output Device (输出设备)
      - Display (显示器)
      - Speaker (音响)

几点说明:
- 很多人会认为计算机存储分为RAM和ROM, 如果把RAM理解为内存条, 那么硬盘就变成了ROM, 其实这句话应该这样说:计算机内存包括RAM和ROM, 硬盘是外部设备, 换句话说硬盘都不是内存, 也就简单了
- 对于单片机来说RAM和ROM都集成在了单片机中, 当程序足够放在ROM时则不需要外设, 而程序通过ISP直接写到ROM中, MCU上电后直接运行ROM中0000H的instruction(指令)
- 对于Computer, 就是我们平时用的电脑来说, RAM是内存条, 而ROM则是由CMOS作为介质的设备, 其中写入的程序称为BIOS, 是由生产商提供的硬件引导程序, 通过BIOS引导到硬盘上, 进而把操作系统引导起来
- 我们平时双击运行程序, 可以理解为操作系统将软件image加载进内存条(实则是主存的RAM), 所以说内存条这个说法也挺害人的, 为什么要加载呢? 因为CPU运行硬盘上的指令太慢, 和RAM差太多了, 但是单片机运行程序则不需要从ROM中加载到RAM中, 第一可以直接寻址, 第二ROM足够快
- 单片机中的ROM和U盘都采用EEPROM作为存储媒介, 但单片机中的EEPROM就上升为ROM, 而U盘就是外部设备, 所以这个就和CPU寻址有直接关系


## Transistor (晶体管)

整个计算机中最重要的就是晶体管, 事实上晶体管可以理解为一个没有机械结构的开关(switch), 通过一个弱小的电流控制开关的打开和闭合。

推荐这个视频 [Transistors, How do they work ? - YouTube](https://www.youtube.com/watch?v=7ukDKVHnac4), 墙内就这个[链接(bilibili)](https://www.bilibili.com/video/av9735297)

- Semiconductor (半导体)
- 硅(Si)是四键, 通过和其他元素混合形成特定效果
- N-type DOPING (N型参杂, 参杂五键的麟(Boracium, B))
- P-type DOPING (P型参杂, 参杂三键的硼(Phosphorum, P))
- BJT (双极性晶体管) 和 FET (场效应晶体管)
- 整个计算逻辑都是在晶体管之间完成


## 0和1是如何转化为电的?

其实从来就是电, 整个计算机都是电的世界, CPU的输入输出以及存储都是采用电的形式, 0和1的世界是虚构出来, 最终的物理载体就是电信号。

换句话说, 我们是用一种意识在操纵整个电路。

见知乎讨论
[代码是如何控制硬件的？ - 知乎](https://www.zhihu.com/question/20492284/answer/15279863)

### 参考阅读
- [计算机是如何启动的？- 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2013/02/booting.html)
- [计算机是如何启动的？- Misaka.r.Me](http://www.misakar.me/neox2/)


> 最后更新时间: 14 Oct 2019