[English](/README.md) | [ 简体中文](/README_zh-Hans.md) | [繁體中文](/README_zh-Hant.md) | [日本語](/README_ja.md) | [Deutsch](/README_de.md) | [한국어](/README_ko.md)

<div align=center>
<img src="/doc/image/logo.svg" width="400" height="150"/>
</div>

## LibDriver BH1750FVI

[![MISRA](https://img.shields.io/badge/misra-compliant-brightgreen.svg)](/misra/README.md) [![API](https://img.shields.io/badge/api-reference-blue.svg)](https://www.libdriver.com/docs/bh1750fvi/index.html) [![License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](/LICENSE)

BH1750FVI是用于I2C总线接口的数字环境光传感器IC。该集成电路最适合获取环境光数据，用于调整手机的LCD和键盘背光功率。可以在高分辨率下检测宽范围。它可用于手机、液晶电视、笔记本电脑、便携式游戏机、数码相机、数码摄像机、PDA、LCD显示器等。

LibDriver BH1750FVI是LibDriver推出的BH1750FVI的全功能驱动，该驱动提供连续模式光照读取、单次模式光照读取等功能并且它符合MISRA标准。

### 目录

  - [说明](#说明)
  - [安装](#安装)
  - [使用](#使用)
    - [example basic](#example-basic)
    - [example shot](#example-shot)
  - [文档](#文档)
  - [贡献](#贡献)
  - [版权](#版权)
  - [联系我们](#联系我们)

### 说明

/src目录包含了LibDriver BH1750FVI的源文件。

/interface目录包含了LibDriver BH1750FVI与平台无关的IIC总线模板。

/test目录包含了LibDriver BH1750FVI驱动测试程序，该程序可以简单的测试芯片必要功能。

/example目录包含了LibDriver BH1750FVI编程范例。

/doc目录包含了LibDriver BH1750FVI离线文档。

/datasheet目录包含了BH1750FVI数据手册。

/project目录包含了常用Linux与单片机开发板的工程样例。所有工程均采用shell脚本作为调试方法，详细内容可参考每个工程里面的README.md。

/misra目录包含了LibDriver MISRA代码扫描结果。

### 安装

参考/interface目录下与平台无关的IIC总线模板，完成指定平台的IIC总线驱动。

将/src目录，/interface目录和/example目录加入工程。

### 使用

#### example basic

```C
#include "driver_bh1750fvi_basic.h"

uint8_t res;
uint32_t i, times;
bh1750fvi_address_t address;

/* set hardware params */
times = 3;
address = BH1750FVI_ADDRESS_LOW;

...
    
/* basic init */
res = bh1750fvi_basic_init(address);
if (res != 0)
{
    return 1;
}

/* delay 1000ms */
bh1750fvi_interface_delay_ms(1000);

...
    
for (i = 0; i < times; i++)
{
    float lux;

    /* basic read */
    res = bh1750fvi_basic_read(&lux);
    if (res != 0)
    {
        (void)bh1750fvi_basic_deinit();
        
        return 1;
    }

    /* output */
    bh1750fvi_interface_debug_print("%d/%d.\n", i + 1, times);
    bh1750fvi_interface_debug_print("%.2flux.\n", lux);

    /* delay 1000ms */
    bh1750fvi_interface_delay_ms(1000);
    
    ...
}

...
    
(void)bh1750fvi_basic_deinit();

return 0;
```

#### example shot

```C
#include "driver_bh1750fvi_shot.h"

uint8_t res;
uint32_t i, times;
bh1750fvi_address_t address;

/* set hardware params */
times = 3;
address = BH1750FVI_ADDRESS_LOW;

...
    
/* shot init */
res = bh1750fvi_shot_init(address);
if (res != 0)
{
    return 1;
}

...
    
for (i = 0; i < times; i++)
{
    float lux;

    /* shot read */
    res = bh1750fvi_shot_read(&lux);
    if (res != 0)
    {
        (void)bh1750fvi_shot_deinit();
        
        return 1;
    }

    /* output */
    bh1750fvi_interface_debug_print("%d/%d.\n", i + 1, times);
    bh1750fvi_interface_debug_print("%.2flux.\n", lux);

    /* delay 1000ms */
    bh1750fvi_interface_delay_ms(1000);
    
    ...
}

...
    
(void)bh1750fvi_shot_deinit();

return 0;
```

### 文档

在线文档: [https://www.libdriver.com/docs/bh1750fvi/index.html](https://www.libdriver.com/docs/bh1750fvi/index.html)。

离线文档: /doc/html/index.html。

### 贡献

请参考CONTRIBUTING.md。

### 版权

版权 (c) 2015 - 现在 LibDriver 版权所有

MIT 许可证（MIT）

特此免费授予任何获得本软件副本和相关文档文件（下称“软件”）的人不受限制地处置该软件的权利，包括不受限制地使用、复制、修改、合并、发布、分发、转授许可和/或出售该软件副本，以及再授权被配发了本软件的人如上的权利，须在下列条件下：

上述版权声明和本许可声明应包含在该软件的所有副本或实质成分中。

本软件是“如此”提供的，没有任何形式的明示或暗示的保证，包括但不限于对适销性、特定用途的适用性和不侵权的保证。在任何情况下，作者或版权持有人都不对任何索赔、损害或其他责任负责，无论这些追责来自合同、侵权或其它行为中，还是产生于、源于或有关于本软件以及本软件的使用或其它处置。

### 联系我们

请联系lishifenging@outlook.com。