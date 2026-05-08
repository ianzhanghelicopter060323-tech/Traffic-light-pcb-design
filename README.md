# 功能扇区摘要
## 扇区功能表
- 注意```Voice_Input```需要语音输入部分
- 注意```WS2812_Display_Interface```不使用256个LED，需要屏幕选型

| 功能扇区                     |   是否必须 | 主要内容                                      |
| ------------------------ | -----: | ----------------------------------------- |
| Battery_Input_Protection |     必须 | 电池接口、开关、保险丝、反接保护、TVS                      |
| Power_5V_LED             |     必须 | 大电流 Buck、屏幕供电电容、LED 电源测试点                 |
| Power_CSK5062            |     必须 | CSK5062 VCC 供电、去耦、VDD_IO/VDD_CORE/VMID 电容 |
| CSK5062_Min_System       |     必须 | CSK5062、晶振预留、启动配置、基础 GPIO                 |
| Voice_Input              |     必须 | 麦克风、偏置、RC 滤波、MIC_P/MIC_N                  |
| WS2812_Display_Interface | 必须，最重要 | 5V/GND/DATA 接口、串联电阻、电平转换、ESD、大电容          |
| UART_Boot_Debug          |     必须 | BOOT_TXD、BOOT_RXD、GND、VCC、BOOT 按键         |
| Test_And_Service         |     推荐 | 电源测试点、DATA 测试点、GPIO 测试点                   |
| Mechanical_Silkscreen    |     必须 | 队伍名称、安装孔、接口方向标注、禁止厂商 LOGO                 |


## 功能扇区架构图
```
电池
 │
 ├── 反接保护 / 保险丝 / 开关
 │
 ├── Buck 5V_LED ────────────────┬── WS2812 屏幕接口 VCC
 │                               ├── 屏幕接口大电容
 │                               └── 电平转换器 5V 供电
 │
 └── CSK5062 VCC 电源
        │
        ├── CSK5062 最小系统
        │     ├── VCC 4.7uF
        │     ├── VDD_IO 2.2uF
        │     ├── VDD_CORE 1uF
        │     ├── VMID 1uF
        │     └── 24MHz 晶体预留
        │
        ├── 麦克风输入 MIC_P / MIC_N
        │
        ├── LED_DATA GPIO
        │       └── 3.3V → 5V 电平转换 → 串联电阻 → WS2812 DIN
        │
        └── UART Boot / Debug
                ├── BOOT_TXD / GPIOA_00
                ├── BOOT_RXD / GPIOA_01
                └── BOOT 按键
```
## 下载方式
```
按住 BOOT
↓
按一下 RESET，或重新上电
↓
松开 BOOT
↓
进入 Boot 下载模式
```
- 进入下载模式后，串口烧录
- 只需要使用```TXD``` ```RXD``` ```GND```即可烧录
- 禁止将```VDD_IO_REF```连任何电源