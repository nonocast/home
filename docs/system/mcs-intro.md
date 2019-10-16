# 单片机是什么?

- 一般将性能相对较低的嵌入式处理器归为微控制器(Micro Control Unit, MCU), 也就说我们说的单片机。
- 微处理器(Microprocessor, 也被称为Center Process Unit, 即CPU)和微控制器(MCU)的主要区别是CPU不包含Memory和I/O, 我们之前说过一个计算机系统需要有CPU, Memory和I/O组成, 而MCU就是在一个片上同时集成了CPU, Memory和I/O, 满足了特定系统的需要
- CPU, MCU从根本上来说都是集成电路(IC, integrated circuit), 或称微电路(microcircuit), 微芯片(microchip), 芯片(chip), 换句话说, 芯片(chip)就是内含集成电路的硅片, 从抽象层面可以理解为将原本在电路板(PCB)实现的电路缩小在一个晶片上
- 集成电路(IC)对于离散晶体管有2个主要优势: 成本和性能。成本低是由于芯片把所有的元件通过照相平版技术，作为一个单位印刷，而不是在一个时间只制作一个晶体管。性能高是由于元件快速开关，消耗更低能量，因为元件很小且彼此靠近。2006年，芯片面积从几平方毫米到350 mm²，每mm²可以达到一百万个晶体管
- 晶体管(transistor)被认为是现代历史中最伟大的发明之一, 可能是二十世纪最重要的发明, 它原本需要几个房间那么大的机器变得只有信用卡那么大, 好比说手机。所以说晶体管是现代计算机的最小单位 [二极管、三极管、场效应管的原理和特征](https://blog.csdn.net/u012271722/article/details/38625875)

## 8051

> The Intel 8051AH is a MCS-51 NMOS single-chip 8-bit microcontroller with 32 I/O lines, 2 Timers/Counters, 5 Interrupts/2 priority levels 4 KB ROM, 128 Bytes on-chip RAM.

早在1981年, Intel就生产了8位微控制器, 命名为8051。8051中集成了18B RAM, 4KB ROM, 两个定时器, 一个串口以及4个端口(每个端口8位), 8位以为着CPU一次只能处理8个bit。

当时因为版权问题所以每家生产的机器指令不相同也能相同, 但是后来Intel忙着去开发更高级的CPU, 也没心思管了, 就将8051授权给没能力设计芯片的制造商去生产, 也就意味着只要是为一家8051芯片编程, 就同时可以运行在其他制造商生产的8051上运行。

8051是MCS-51中最初的一个产品, 这个系列也包括了8052, 8031等MCU。

## STC89C52RC

国内现在接触最多的应该是STC的单片机, 如果想有一块单片机最简单的方法就是京东上直买[《51单片机项目教程（C语言版）（赠单片机开发板）》- 京东图书](https://item.jd.com/11967011.html) 79.60直接送一块板子，物超所值。

硬件和软件不一样, 要了解一个单片机最好的方式就是学习它的Datasheet, 直接去宏晶的网站下载就行。

STC89C52RC
- 2004年推出增强型8051单片机, 6时钟每机器周期和12时钟每机器周期可任意选择, 指令代码完全兼容传统8051
- 工作频率范围: 0~35MHz, 相当于普通8051的0~70MHz, 实际工作频率可达42MHz, 具体的机器周期取决于给MCU搭配的晶振
- STC: 宏晶科技
- 89: 表示采用6T/12T 8051
- C: 5.5V ~ 3.8V
- 52: 8k字节的ROM和512B的RAM
- RC: 自带RC时钟振荡电路

结合stcgal交叉观察,
```
$ stcgal -P stc89 -p /dev/tty.usbserial-14310
Target model:
  Name: STC89C52RC/LE52R
  Magic: F002
  Code flash: 8.0 KB
  EEPROM flash: 6.0 KB
Target frequency: 11.016 MHz
Target BSL version: 4.3C
```

在18,19引脚外接11.0592MHz的晶振得到的信息如下:
- CPU:
  - 8bit (ALU, register, data bus的bit width都是8bit，所以说是8位CPU, address bus是16bit)
  - Clock cycle (时钟周期): 11.0592MHz, 即1个cycle是1/12us (微秒), 每秒输出1200万次 (i7已经每秒4亿次了)
  - Instruction cycle (指令周期): 12 x Clock cycle = 1/12usx12=1us, 正好1个us
- RAM: SRAM, 512B (物理和逻辑上都分为两个地址空间: 内部256B, 内部扩展256B, 不同型号的会有所区别，但是内部固定256B)
- ROM: 也叫做Code flash，程序存储区, 采用EEPROM flash 8K (address: 0000H-1FFFH)
- STORAGE: 采用EEPROM flash，容量为6KB (address: 2000H-AFFFH)
- I/O: 32pin
- UART: 1

上面说的RAM和ROM构成主存/内存, 而STORAGE可以理解为外部设备, 辅助存储。

## RAM和寄存器

按一般逻辑来说, 寄存器(Register)和CACHE都是在CPU内部的, 但现在是MCU, 所以寄存器就共用了RAM的介质。

STC89C52RC有512B的RAM，其中内部256B，内部又分为3个部分:
- 低128B (与传统8051兼容), 也称为通用RAM区
- 高128B (Intel在8052扩展了高128B)
- sfr (特殊功能寄存器)
高128B和sfr物理上是2个空间，反正这里我也没整明白，难道有2个128B的物理空间, 共享地址这个比较容易理解，sfr必须直接寻址，而高128B则需要间接寻址。
低128B的前32B包含4组通用寄存器组，每组8个B，分别是R0-R7，然后从20H-2FH (16B, 128b) 可按位寻址，

特殊寄存器就是单片机打通硬件和软件的核心区域，书上最多的就是点亮LED灯，

app.c
```c
sbit light = 0x90;
void main() {
  light = 0;
  while(1) {}
}
```
这个0x90就是对应到RAM的第90个bit, 将这个bit设置为0, 进而触发第一个单片机引脚低电压, 在VCC之间形成电压差产生电流。

仿真后也可以直观的看到D:90H从FF变为FE, 最低位置0。

对应的汇编其实就更加直白,

app.asm
```asm
ORG 0H
CLR 90H
HERE: SJMP HERE
END
```

是不是更加直接?
你可以观察一下生成的二进制(hex), 一共就4个byte
```
C2 90 80 FE
```
然后对应STC89C52RC中的Datasheet p87
```
CLR bit
功能: 清零指定的位
指令长度: 2个字节
二进制编码： 1100 0010 [bit address]
```

我们可以看到上面的C2 90, C2对应的bit: 1100 0010, 后面的90就是P1_1, 机器指令也够直接把。

SJMP的指令2个字节, 1000 0000 [rel.address]
第三个字节80就是1000 0000, FE对应1111 1110, 就是-1, 因为SJMP的范围是[-127, 128], PC运行后会自动+1，现在再把你减回来等于无限循环。

所以一个最简单的hex就是80 FE, 亮灯就是C2 90，直接写了发下去。
hey.ihx
```
:04002000C29080FE0C
:00000001FF
```
然后下发，
```
stcgal --debug -P stc89 -p ${DEVICE} app.ihx
```

如果是Windows就直接hexedit写四个字节就完事了。

这一圈算是把STC89C52RC看了一下，单片机内部的硬件我们放一放，等到看具体功能再一个个看，这是我的弱项，什么锁存器，什么上拉电阻，头晕。

最后补充一下，windows和mac两个环境,
- mac可以下发但是不能仿真 (sdcc/stcgal)
- windows可以仿真但是不能下发 (keil/stcisp)
所以挺好, 两边的环境都接触一下，anyway, ihx和hex一定是一样的，只是当中的C和汇编语法有所区别。

到了这里往下就是proteus, 随便画个图把刚才的程序导入进去就可以运行

![Screen Shot 2019-10-06 at 9 09 29 PM](https://user-images.githubusercontent.com/1457904/66269686-f88c2180-e87d-11e9-9222-8573d2122db3.jpg)