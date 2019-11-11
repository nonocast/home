# 中断和时钟

CPU默认根据ROM中的指令顺序执行, 中断相当于暂停CPU当前运行的顺序, 改而去运行一段对应的指令序列, 执行完成后会继续运行之前的指令。

8051有5个可用中断:
- 复位
- 外部硬件中断0 (INT0)
- 外部硬件中断1 (INT1)
- 定时器0中断 (TF0)
- 定时器1中断 (TF1)
- 串口中断 （R1和T1)

## 外部中断 （INT0 & INT1)

- INT0对应P3.2
- INT1对应P3.3

app.c

```c
EX0 = 1;    // 启用INT0
EA = 1;     // 启用全局中断
IT0 = 0;    // 低电平触发
```

这3句分别是设置了3个bit, 打开了INT0, 同时设定为低电平触发, INT0有2种触发方式: 低电平触发和下降沿触发。

仔细理解2者的区别, 其实很简单,

- 低电平触发, 就是给引脚P3.2一个低电平就会一直触发中断
- 下降沿触发, 就是引脚P3.2感知到从高电平到低电平这个过程的一刹那才会触发一次中断

可以理解低电平触发模式是一个持续的过程, 而下降沿是一个瞬间过程。

完整的代码如下,
```c
#include <8052.h>

#define true 1
#define false 0

#define low 0;
#define high 1;

typedef int BOOL;
typedef unsigned char BYTE;
typedef unsigned int WORD;

void delay(unsigned int);
void init();
void initLights();

void loop();

void main() {
  init();
  loop();
}

void init() {
  initLights();

  EX0 = 1;
  EA = 1;
  IT0 = 0;
}

void loop() {
  while (true) {
  }
}

void uart() __interrupt(0) {
  P1 = ~P1;
  delay(200);
}

void initLights() {
  P1 = 0xf0;
  delay(500);
  P1 = 0x0f;
}

void delay(unsigned int i) {
  unsigned char j;
  for (i; i > 0; i--)
    for (j = 100; j > 0; j--)
      ;
}
```




